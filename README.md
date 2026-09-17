# Minicurso de Git e GitHub: do básico ao avançado

Este é o repositório do minicurso de Git e GitHub do projeto **SIRC**, da **Universidade Franciscana (UFN)**.

O curso começa do zero, com os primeiros comandos do Git, e vai até o fluxo de trabalho usado em equipes: branches, Pull Requests e resolução de conflitos. Tudo é praticado neste repositório.

## O que você vai aprender

**Básico**
- O que é controle de versão e por que usar o Git
- Configurar o Git e criar ou clonar um repositório
- Registrar mudanças com `git add` e `git commit`
- Ver o histórico com `git status`, `git log` e `git diff`

**Intermediário**
- Criar, trocar e apagar branches
- Juntar branches com `git merge` e resolver conflitos
- Trabalhar com o GitHub: `git push`, `git pull` e `git fetch`
- Ignorar arquivos com o `.gitignore`

**Avançado**
- Desfazer mudanças com `git restore`, `git reset` e `git revert`
- Guardar trabalho temporário com `git stash`
- Reorganizar o histórico com `git rebase` e `git cherry-pick`
- Abrir e revisar Pull Requests, também pela ferramenta de linha de comando do GitHub (`gh`)
- Criar tags para marcar versões

## Conteúdo do repositório

| Arquivo | Para que serve |
| --- | --- |
| [notas.md](notas.md) | Guia de consulta com os principais comandos de Git e GitHub |
| [main.py](main.py) e [parouimpar.py](parouimpar.py) | Programa em Python usado nos exercícios: diz se um número é par ou ímpar |
| [rosto.md](rosto.md) | Desenho em texto (uma carinha) usado nos primeiros exercícios de commit |
| [fazer.txt](fazer.txt) | Arquivo usado para praticar mudanças e commits |

## Pré-requisitos

- [Git](https://git-scm.com/downloads) instalado
- Uma conta no [GitHub](https://github.com)
- [Python 3](https://www.python.org/downloads/) para rodar o exemplo
- Um editor de código, como o [VS Code](https://code.visualstudio.com/)

## Como começar

```bash
git clone <url-deste-repositorio>
cd MiniCursoSIRC-git
python3 main.py
```

Depois, abra o [notas.md](notas.md) e siga os comandos enquanto acompanha o curso.

## Como praticar

1. Crie uma branch para o seu exercício: `git switch -c meu-exercicio`
2. Faça suas alterações e registre com `git add` e `git commit`
3. Envie para o GitHub: `git push -u origin meu-exercicio`
4. Abra um Pull Request para a `main`

---

Projeto SIRC · Universidade Franciscana (UFN)
