# 🚀 Fluxo de Desenvolvimento Git (Senior Level)

Este repositório segue um **fluxo profissional de desenvolvimento**, projetado para trabalhar com **múltiplos desenvolvedores, QA e deploy seguro em produção**.

---

## 🧠 Visão Geral do Fluxo

```
JIRA (Planejamento)
   ↓
feature/* (Desenvolvimento)
   ↓ PR
develop (Integração)
   ↓
release/* (Congelamento)
   ↓
main (Produção)
```

---

## 🧩 Papéis no Processo

| Papel | Responsabilidade |
|-----|----------------|
| Dev | Implementar features e correções |
| Reviewer | Revisar código |
| QA | Validar funcionalidades nos ambientes |
| Tech Lead | Aprovar releases |
| CI/CD | Garantir qualidade automática |

---

## 🌱 Branches Principais

| Branch | Finalidade |
|------|----------|
| `feature/*` | Desenvolvimento de funcionalidades |
| `develop` | Integração contínua |
| `release/*` | Código congelado para QA final |
| `main` | Produção |

---

## 🔹 1. Planejamento (JIRA)

- Todo trabalho nasce em um ticket do JIRA  
- Exemplo: `SPM-322 – Filtrar bots nas métricas`
- **1 ticket = 1 branch**

> O JIRA é a fonte da verdade do processo.

---

## 🔹 2. Desenvolvimento

Criar branch a partir da `develop`:

```bash
git checkout develop
git pull
git checkout -b feature/SPM-322-filtrar-bots
```

Boas práticas:
- Commits pequenos
- Commits sem quebrar build
- Mensagens claras

---

## 🔹 3. Pull Request (feature → develop)

- PR obrigatório
- Pelo menos **1 reviewer**
- **CI precisa passar**
- Merge via **Squash** ou **Rebase**

> QA **não aprova PR**, QA valida ambientes.

---

## 🔹 4. QA de Integração (QA-INT)

- Deploy automático da `develop`
- Ambiente instável
- Testes rápidos e exploratórios

---

## 🔹 5. Release (Congelamento)

Criada em data definida (ex: semanal):

```bash
git checkout develop
git pull
git checkout -b release/2026-01-22
git push origin release/2026-01-22
```

Regras:
- Nenhuma feature nova
- Apenas correções

---

## 🔹 6. QA de Release (QA-REL)

- Deploy do `release/*`
- Testes completos
- Regressão
- Ambiente estável

### Bugs encontrados?
- Criar ticket no JIRA
- Branch a partir da release:

```bash
fix/SPM-340-fix-metric
```

---

## 🔹 7. Produção (main)

Quando QA e Tech Lead aprovarem:

```bash
git checkout main
git merge release/2026-01-22
git push origin main
```

- Deploy automático
- Produção real

---

## 🔁 8. Back-Merge (Obrigatório)

Garante que correções não se percam:

```bash
git checkout develop
git merge release/2026-01-22
git push origin develop
```

---

## 🔐 Proteção de Branches

### `develop`
- PR obrigatório
- CI obrigatório
- 1 reviewer

### `release/*`
- PR obrigatório
- CI obrigatório

### `main`
- PR obrigatório
- CI obrigatório
- Aprovação Tech Lead

---

## 🧠 Boas Práticas Avançadas

- Feature Flags para deploy seguro
- CI como gate obrigatório
- Nunca commitar direto em `main` ou `develop`
- Releases pequenas e frequentes

---

## 🎯 Quando algo vai para Produção?

> **Somente quando passar por:**
1. feature/*
2. develop
3. QA-INT
4. release/*
5. QA-REL
6. main

---

## ✅ Objetivo do Fluxo

- Evitar conflitos
- Garantir qualidade
- Escalar time com segurança
- Produzir com previsibilidade

---

**Este fluxo representa um padrão usado em times profissionais e ambientes de produção.**
