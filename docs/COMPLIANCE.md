# Conformidade automatizada no CI

Este documento mapeia cada verificação automática do CI para o requisito que ela ajuda a cobrir.
É um apoio à conformidade, não uma declaração de conformidade.

## Mapeamento

| Verificação (workflow) | O que detecta | Requisito que ajuda a cobrir |
|---|---|---|
| gitleaks (`security.yml`) | Segredos no código e no histórico git | ABNT NBR ISO/IEC 27001 e 27002 (gestão de credenciais) |
| CodeQL (`security.yml`) | Vulnerabilidades no código-fonte | ABNT NBR ISO/IEC 27002 (desenvolvimento seguro); ABNT NBR ISO/IEC 25010 (segurança) |
| Dependency review, npm audit, pip-audit, govulncheck, Trivy (`security.yml`) | Dependências e imagens com vulnerabilidades conhecidas | ABNT NBR ISO/IEC 27002 (gestão de vulnerabilidades técnicas); ABNT NBR ISO/IEC 25010 (segurança) |
| Dependabot (`dependabot.yml`) | Dependências e actions desatualizadas | ABNT NBR ISO/IEC 27002 (gestão de vulnerabilidades); ABNT NBR ISO/IEC 25010 (manutenibilidade) |
| Logs com dados pessoais ou credenciais (`privacy-session-checks.yml`) | `console.log`/`print` com cpf, senha, token, cartão | LGPD (Lei 13.709/2018), arts. 6º e 46 |
| CPF/CNPJ reais hardcoded (`privacy-session-checks.yml`) | Números válidos com máscara fora de testes | LGPD, arts. 6º e 46 (minimização e segurança) |
| Cookies sem HttpOnly, Secure, SameSite (`privacy-session-checks.yml`) | Criação de cookie de sessão sem flags | ABNT NBR ISO/IEC 27002 (sessão); ABNT NBR ISO/IEC 25010 (segurança) |
| Segredo fixo, TLS desabilitado, CORS com credenciais, debug em produção (`privacy-session-checks.yml`) | Configurações inseguras no código | ABNT NBR ISO/IEC 27001 e 27002; ABNT NBR ISO/IEC 25010 (segurança) |
| `.env` versionado (`privacy-session-checks.yml`) | Arquivo de ambiente no git | LGPD, art. 46; ABNT NBR ISO/IEC 27002 (gestão de credenciais) |
| `SECURITY.md` e `PRIVACY.md` (aviso) | Presença de política de segurança e de privacidade | LGPD (transparência); ABNT NBR ISO/IEC 27001 (políticas) |
| axe-core WCAG 2.2 A/AA (`accessibility-quality.yml`) | Violações automatizáveis de acessibilidade | WCAG 2.2 nível AA; base da ABNT NBR 17225 e do eMAG |
| `lang="pt-BR"` (`accessibility-quality.yml`) | Idioma da página declarado | WCAG 3.1.1 (nível A); eMAG |
| Título do PR em Conventional Commits (`commit-lint.yml`) | Padrão de título | ABNT NBR ISO/IEC 25010 (manutenibilidade, rastreabilidade) |
| Sem trailers de co-autoria de IA nos commits (`commit-lint.yml`) | `Co-authored-by:` e `Generated with` | Política interna do repositório (autoria e rastreabilidade) |

## O que o CI NÃO cobre

- Auditoria humana de segurança, de privacidade e de acessibilidade.
- Encarregado de dados (DPO), base legal de cada tratamento e Relatório de Impacto à Proteção de Dados Pessoais (RIPD), exigidos pela LGPD.
- Testes de invasão (pentest) e revisão de modelo de ameaças (threat model).
- Certificação ABNT NBR ISO/IEC 27001, avaliação formal de qualidade ABNT NBR ISO/IEC 25010 e atestado de conformidade eMAG ou ABNT NBR 17225.
- Testes com usuários reais e com tecnologias assistivas (leitores de tela, navegação por teclado).
- Análise de fluxo de dados pessoais, retenção e descarte. As heurísticas são por padrão de texto e podem gerar falsos positivos ou negativos.
- Segurança em tempo de execução, em infraestrutura e em configuração de produção.
