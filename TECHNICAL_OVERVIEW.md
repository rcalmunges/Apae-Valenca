
# 🧠 Detalhamento Técnico e Tópicos de Estudo

Este documento serve como um guia para desenvolvedores e recrutadores entenderem a profundidade técnica aplicada neste projeto. Aqui estão os principais conceitos de Engenharia de Software utilizados.

---

## 1. Gerenciamento de Estado e Performance (React)

### Context API
Utiliei a Context API para evitar *Prop Drilling* em estados globais essenciais.
- **`ToastContext`:** Sistema de notificações global. Disparar feedbacks visuais (`success`, `error`) de qualquer componente sem acoplamento.
- **`DonationContext`:** Controla o modal de doação que pode ser acionado de qualquer ponto da aplicação (Header, Footer, CTA).

### Otimização de Renderização
- **`React.lazy` e `Suspense`:** Implementação de *Code Splitting* nas rotas. O bundle inicial carrega apenas o necessário, e as outras páginas (como o Painel Admin) são baixadas sob demanda, melhorando o *Core Web Vitals (LCP)*.
- **`useMemo` e `useCallback`:** Utilizados extensivamente em listas filtradas (ex: Dashboard Financeiro, Blog) para evitar recálculos pesados e re-renderizações desnecessárias de componentes filhos.

---

## 2. Padrões de Projeto e Arquitetura

### Componentização
Adotei o padrão de componentes "burros" (apresentação) e "inteligentes" (contêineres de lógica), embora com o uso de Hooks, essa linha seja tênue.
- **Componentes Atômicos:** `WhatsAppButton`, `PageLoader`, `SEO`.
- **Componentes Compostos:** `AdminModal` (que gerencia formulários complexos dinamicamente baseado em props).

### Custom Hooks & Services
A lógica de negócios e chamadas externas foi separada da UI.
- **`supabaseClient.ts`:** Singleton para conexão com o banco, garantindo uma única instância do cliente.
- **`auditLogger.ts`:** Serviço utilitário desacoplado para registrar ações do usuário, podendo ser injetado em qualquer fluxo crítico (Create/Update/Delete).

---

## 3. Segurança e Dados

### Autenticação e Proteção de Rotas
- Implementação de um componente **`ProtectedRoute`** (HOC - Higher Order Component pattern) que verifica a sessão do usuário antes de renderizar rotas administrativas.
- Redirecionamento automático para login caso o token expire.

### Tratamento de Dados Sensíveis
- Uso de variáveis de ambiente (`import.meta.env`) para chaves de API.
- Sanitização de inputs nos formulários antes do envio.
- **Row Level Security (RLS):** No lado do Supabase, regras estritas garantem que apenas usuários autenticados com a *role* correta possam escrever no banco.

---

## 4. Integrações e Manipulação de Arquivos

### Geração de Documentos (Client-Side)
Uma das *features* mais complexas é a geração de PDFs no frontend sem necessidade de backend server.
- **Lógica:** O arquivo `pdfGenerator.ts` contém algoritmos para calcular quebras de página, desenhar tabelas dinâmicas e renderizar imagens base64 dentro do canvas do PDF.

### Manipulação de Imagens
- Componente `ImageUpload` com preview em tempo real.
- Suporte a Drag-and-Drop.
- Conversão de arquivos para Base64 para envio via JSON payloads (integração Google Apps Script) ou upload direto via `FormData` para o Supabase Storage.

---

## 5. Qualidade de Código (TypeScript)

Utilizei no projeto TypeScript em modo estrito.
- **Interfaces:** Definição clara de modelos de dados (`UserProfile`, `Transaction`, `Schedule`) no arquivo `types.ts`.
- **Tipagem de Props:** Todos os componentes React possuem interfaces de Props definidas, prevenindo erros de tipagem durante o desenvolvimento.
- **Null Safety:** Tratamento extensivo de valores `null` ou `undefined` vindos da API.

---

## 📊 Estrutura de Banco de Dados (Supabase)

O projeto utiliza um banco relacional PostgreSQL com as seguintes tabelas principais:

1.  **`profiles`**: Extensão da tabela de auth, armazenando roles (`admin`, `profissional`) e metadados.
2.  **`family_registrations`**: Dados complexos de matrícula (JSONB support).
3.  **`schedules`**: Agenda com relacionamento FK para `profiles` (profissional) e `family_registrations` (paciente).
4.  **`audit_logs`**: Tabela de log imutável para segurança.
