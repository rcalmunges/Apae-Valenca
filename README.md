
# 💙 Plataforma Digital - APAE Valença

![Status](https://img.shields.io/badge/Status-Produção-green)
![Versão](https://img.shields.io/badge/Versão-1.0.0-blue)
![Licença](https://img.shields.io/badge/Licença-MIT-lightgrey)

> **Uma Solução SPA (Single Page Application) completa para gestão institucional, doações e transparência.**

---

## 📸 Visão Geral

Este projeto foi desenvolvido para modernizar a infraestrutura digital da **APAE Valença**, substituindo processos manuais por um sistema integrado e acessível. A aplicação conecta a comunidade à instituição, facilita a captação de recursos e oferece um painel administrativo robusto para gestão interna.

### 🔗 Links
- **Deploy (Online):** [Acesse o Site Oficial](https://apaevalencaba.org.br)
- **Documentação Técnica:** [Ver Arquitetura](TECHNICAL_OVERVIEW.md)

---

## 🚀 Tecnologias e Skills Aplicadas

O projeto foi construído utilizando uma stack moderna, focada em performance, tipagem estática e escalabilidade.

### Frontend (Core)
- **React 19:** Utilização de Hooks avançados (`useCallback`, `useMemo`, `useContext`) para gerenciamento de estado e performance.
- **TypeScript:** Tipagem estrita para garantir a integridade dos dados e reduzir bugs em tempo de execução.
- **Vite:** Build tool de última geração para desenvolvimento rápido e otimizado.

### Estilização e UI
- **Tailwind CSS:** Design responsivo, *Dark Mode* nativo e customização via tokens.
- **Lucide React:** Ícones vetoriais leves e consistentes.
- **Design Responsivo:** Layout adaptável (Mobile-First) com menu hambúrguer e grids flexíveis.

### Backend & Integração
- **Supabase:** Utilizado como Backend-as-a-Service (BaaS).
  - **Auth:** Sistema de login seguro e persistência de sessão.
  - **Database:** PostgreSQL para dados relacionais (Matrículas, Financeiro, Blog).
  - **Storage:** Armazenamento de imagens e documentos.
  - **RLS (Row Level Security):** Regras de segurança a nível de banco de dados.

### Funcionalidades Avançadas
- **Geração de PDF no Frontend:** Uso de `jspdf` e `jspdf-autotable` para gerar fichas de matrícula e relatórios financeiros diretamente no navegador.
- **Google Apps Script:** Integração via Webhook para backup automático de dados críticos no Google Drive/Sheets.
- **API de Voz (Web Speech API):** Recurso de acessibilidade nativo para leitura de tela.

---

## 🛠️ Arquitetura do Projeto

A estrutura de pastas foi organizada para escalabilidade e manutenção:

```bash
src/
├── components/       # Componentes de UI Reutilizáveis (Botões, Modais, Inputs)
│   ├── admin/        # Componentes exclusivos do Painel de Controle
├── context/          # Gerenciamento de Estado Global (Context API)
├── pages/            # Rotas da Aplicação (Lazy Loaded)
├── lib/              # Configurações de serviços externos (Supabase)
├── utils/            # Funções auxiliares (Formatadores, Validadores, Loggers)
└── types.ts          # Definições de Tipos TypeScript (Interfaces Globais)
```

---

## ✨ Funcionalidades de Destaque

### 1. Painel Administrativo Completo
Um dashboard protegido por autenticação onde a equipe pode:
- Gerenciar matrículas e status de alunos.
- Controlar fluxo de caixa (Entradas/Saídas) com gráficos interativos (`Recharts`).
- Publicar notícias e campanhas no site.
- Gerenciar agenda de atendimentos clínicos.

### 2. Acessibilidade (A11y)
O site foi construído seguindo diretrizes WCAG:
- Barra de ferramentas de acessibilidade (Alto Contraste, Tamanho da Fonte).
- Leitor de voz integrado.
- Navegação por teclado e tags ARIA semânticas.

### 3. Sistema de Auditoria
Implementação de um sistema de `Audit Logs` que rastreia quem criou, editou ou excluiu registros, garantindo segurança e rastreabilidade das ações administrativas.

---

## 👨‍💻 Autor

Desenvolvido com foco em excelência técnica e impacto social.

**[Robson Calmunges/GitHub]** - *Full Stack Developer*
