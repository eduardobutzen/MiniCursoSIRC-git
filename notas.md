# Guia rápido de Git e GitHub

## 1. Configuração inicial

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu@email.com"
git config --global init.defaultBranch main
git config --list                 # ver configurações
```

## 2. Criar ou clonar um repositório

```bash
git init                          # cria um repositório na pasta atual
git clone <url>                   # copia um repositório remoto
git clone <url> minha-pasta       # clona para uma pasta com outro nome
```

## 3. Ver o estado e o histórico

```bash
git status                        # arquivos modificados, staged e não rastreados
git log                           # histórico de commits
git log --oneline --graph --all   # histórico resumido, com as branches
git show <commit>                 # detalhes de um commit
git diff                          # mudanças ainda não adicionadas (staged)
git diff --staged                 # mudanças já adicionadas, prontas para commit
git blame arquivo.txt             # quem alterou cada linha
```

## 4. Salvar mudanças (add e commit)

```bash
git add arquivo.txt               # adiciona um arquivo à área de staging
git add .                         # adiciona tudo da pasta atual
git add -p                        # escolhe por partes o que adicionar
git commit -m "mensagem"          # cria o commit
git commit -am "mensagem"         # add + commit (só arquivos já rastreados)
git commit --amend                # corrige o último commit (mensagem ou conteúdo)
```

## 5. Desfazer mudanças

```bash
git restore arquivo.txt           # descarta mudanças não adicionadas no arquivo
git restore --staged arquivo.txt  # tira o arquivo do staging (mantém a mudança)
git reset HEAD~1                  # desfaz o último commit, mantém as mudanças
git reset --hard HEAD~1           # desfaz o último commit e APAGA as mudanças (cuidado!)
git revert <commit>               # cria um novo commit que desfaz outro (seguro para branches já enviadas)
git clean -n                      # mostra arquivos não rastreados que seriam apagados
git clean -fd                     # apaga arquivos e pastas não rastreados (cuidado!)
```

## 6. Guardar mudanças temporariamente (stash)

```bash
git stash                         # guarda as mudanças e limpa a área de trabalho
git stash -u                      # inclui arquivos não rastreados
git stash list                    # lista os stashes
git stash pop                     # aplica o último stash e remove da lista
git stash apply                   # aplica sem remover
git stash drop                    # apaga o último stash
```

## 7. Branches

```bash
git branch                        # lista branches locais
git branch -a                     # lista locais e remotas
git branch nova-branch            # cria uma branch
git switch nova-branch            # muda para a branch
git switch -c nova-branch         # cria e já muda para ela
git checkout -b nova-branch       # forma antiga de criar e mudar
git branch -m novo-nome           # renomeia a branch atual
git branch -d nome                # apaga uma branch já mesclada
git branch -D nome                # força a exclusão
```

### Mais comandos de branches

```bash
git branch -v                     # mostra o último commit de cada branch
git branch -vv                    # mostra também qual branch remota cada uma segue
git branch --merged               # branches já mescladas na atual (dá para apagar)
git branch --no-merged            # branches com trabalho ainda não mesclado
git switch -                      # volta para a branch anterior
git switch -c local origin/remota # cria uma branch local a partir de uma remota
git branch -u origin/nome         # define qual branch remota a atual acompanha
git fetch --prune                 # remove referências a branches apagadas no GitHub
git log main..nova-branch         # commits que estão na nova-branch e não na main
git diff main...nova-branch       # o que mudou na nova-branch desde que saiu da main
```

### Dicas

- A branch é só um ponteiro para um commit: criar uma é rápido e não copia arquivos.
- Use uma branch para cada tarefa (ex.: `feature/login`, `fix/erro-soma`, `par-ou-impar`).
- Faça commit ou `git stash` antes de trocar de branch, para não levar mudanças junto sem querer.
- Mantenha a `main` estável e só traga mudanças para ela por merge ou Pull Request.

## 8. Juntar branches (merge e rebase)

```bash
git switch main
git merge nova-branch             # traz as mudanças da branch para a main
git merge --abort                 # cancela um merge com conflito

git rebase main                   # reaplica os commits da branch atual sobre a main
git rebase --continue             # continua depois de resolver conflitos
git rebase --abort                # cancela o rebase

git cherry-pick <commit>          # copia um commit específico para a branch atual
```

### Resolvendo conflitos

1. `git status` mostra os arquivos em conflito.
2. Abra o arquivo e procure os marcadores `<<<<<<<`, `=======` e `>>>>>>>`.
3. Edite para deixar o conteúdo final e apague os marcadores.
4. `git add arquivo.txt`
5. `git commit` (no merge) ou `git rebase --continue` (no rebase).

## 9. Repositórios remotos (GitHub)

```bash
git remote -v                             # lista os remotos
git remote add origin <url>               # conecta a um repositório no GitHub
git remote set-url origin <nova-url>      # troca a URL do remoto

git fetch                                 # baixa as novidades sem mesclar
git pull                                  # fetch + merge da branch atual
git pull --rebase                         # fetch + rebase (histórico mais limpo)

git push                                  # envia os commits
git push -u origin nova-branch            # primeiro push de uma branch nova (define o upstream)
git push origin --delete nome-branch      # apaga a branch no GitHub
git push --force-with-lease               # força o push de forma mais segura (após rebase/amend)
```

## 10. Tags e versões

```bash
git tag                           # lista as tags
git tag v1.0                      # cria uma tag no commit atual
git tag -a v1.0 -m "Versão 1.0"   # tag anotada
git push origin v1.0              # envia uma tag
git push --tags                   # envia todas as tags
```

## 11. GitHub CLI (`gh`)

```bash
gh auth login                     # faz login no GitHub
gh repo create                    # cria um repositório no GitHub
gh repo clone usuario/repo        # clona um repositório
gh repo view --web                # abre o repositório no navegador

gh pr create                      # abre um Pull Request da branch atual
gh pr list                        # lista os PRs
gh pr checkout 12                 # baixa o PR 12 para revisar localmente
gh pr view 12                     # mostra os detalhes do PR
gh pr merge 12                    # mescla o PR

gh issue create                   # cria uma issue
gh issue list                     # lista as issues
```

## 12. Fluxo de trabalho típico

```bash
git switch main
git pull                              # 1. atualiza a main
git switch -c minha-feature           # 2. cria uma branch para a tarefa
# ... edita os arquivos ...
git status                            # 3. confere o que mudou
git add .
git commit -m "Descreve a mudança"    # 4. faz o commit
git push -u origin minha-feature      # 5. envia para o GitHub
gh pr create                          # 6. abre o Pull Request
# depois que o PR for aprovado e mesclado:
git switch main
git pull
git branch -d minha-feature           # 7. limpa a branch local
```

## 13. Arquivo `.gitignore`

Lista os arquivos que o Git deve ignorar. Exemplo:

```
__pycache__/
*.pyc
.venv/
.env
.vscode/
```

`git rm --cached arquivo` para de rastrear um arquivo que já foi commitado (sem apagá-lo do disco).
