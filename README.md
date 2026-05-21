# Borges Projetos — Landing Page

Site institucional da [Borges Projetos](https://borgesprojetos.com), empresa de prevenção de incêndios (PPCI) com sede em Alvorada/RS e atendimento em toda a região metropolitana de Porto Alegre.

## Stack

- **Vue 3** com `<script setup>` + TypeScript
- **Vite 6** (build + dev server)
- **Tailwind CSS v4** (via `@tailwindcss/vite`)
- **FontAwesome** para ícones de serviços

## Desenvolvimento

```bash
npm install
npm run dev          # http://localhost:5173
npm run build        # vue-tsc + vite build → dist/
npm run preview      # serve dist/ localmente
```

## Estrutura

```
src/
├── App.vue                 # monta Header + landing-page
├── view/landing-page.vue   # orquestra as seções
├── components/
│   ├── Header.vue          # nav fixo + WhatsApp + menu mobile
│   ├── HeroSection.vue     # hero com slideshow de highlights
│   ├── ServicesSection.vue # grid de serviços
│   ├── ClientsSection.vue  # carrossel infinito de clientes
│   ├── ContactSection.vue  # formulário + info de contato
│   └── FooterSection.vue   # rodapé
├── data/                   # conteúdo editável (TS)
│   ├── businessInfo.ts     # nome, telefone, email, endereço
│   ├── services.ts         # serviços oferecidos
│   ├── clients.ts          # clientes exibidos no carrossel
│   ├── companyHighlights.ts# slides do hero
│   └── contactInfo.ts      # blocos de contato com ícones
└── types/                  # interfaces TS (Service, Client, etc.)

public/clients/             # logos dos clientes (servidas por URL absoluta)
```

Toda alteração de **conteúdo** (textos, serviços, clientes, contato) é feita nos arquivos em `src/data/` — sem precisar mexer em componentes.

## Deploy

A imagem Docker (`Dockerfile` na raiz) faz build multi-stage:

1. **Stage builder** (`node:20-alpine`): `npm ci` + `npm run build` → `dist/`
2. **Stage runtime** (`nginx:alpine`): serve `dist/` na porta 80 com `nginx.conf` configurado para SPA (try_files → index.html, cache 1y em assets, headers de segurança)

```bash
docker build -t borgesprojetos:latest .
docker run -p 8080:80 borgesprojetos:latest
```

Em produção, a imagem roda atrás de um reverse proxy (Caddy) com TLS via Cloudflare Origin Certificate, com o domínio `borgesprojetos.com` proxied (CDN) pela Cloudflare.

## Notas

- O formulário de contato hoje só registra no console e exibe `alert` — falta integração com backend/WhatsApp/email.
- Logos dos clientes vivem em `public/clients/` e são referenciadas em `src/data/clients.ts` como caminhos absolutos (`/clients/foo.png`).
