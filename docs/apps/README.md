# kubernetes-labs (apps)

Este README.md guiará você pelos principais passos para configurar, atualizar e trabalhar com este repositório.

---

## O que são Git Submodules?

[Git Submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules) permitem que um repositório Git inclua outros repositórios Git como subdiretórios. Isso é útil para gerenciar projetos que dependem de componentes externos, como bibliotecas ou, neste caso, aplicações separadas e configurações de infraestrutura. Eles apontam para um **commit específico** do repositório externo, garantindo que o seu projeto principal sempre use uma versão testada e estável do submódulo.

---

## Estrutura do Repositório

Este repositório principal, `kubernetes-labs`, contém uma pasta `apps` que hospeda os seguintes submódulos:

* `apps/kubernetes-labs-infra-demo`: Aplicação de demonstração para os laboratórios.
* `apps/kubernetes-labs-infra-cluster`: Configurações de infraestrutura para os clusters Kubernetes.

---

## Primeiros Passos para Desenvolvedores

Siga estes passos para clonar e configurar o projeto em sua máquina local.

### 1. Clonar o Repositório Principal

Para começar, clone o repositório `kubernetes-labs` e seus submódulos de uma vez:

```bash
git clone --recurse-submodules https://github.com/seu-usuario/kubernetes-labs.git
```

* `git clone`: Comando padrão para clonar um repositório Git.
* `--recurse-submodules`: Esta flag é **crucial**. Ela garante que, além do repositório principal, todos os submódulos sejam automaticamente inicializados e atualizados para os commits que o repositório pai espera.

**Alternativa (se você clonou sem `--recurse-submodules`):**

Se você já clonou o repositório sem a flag `--recurse-submodules`, os diretórios dos submódulos (`apps/kubernetes-labs-infra-demo` e `apps/kubernetes-labs-infra-cluster`) estarão vazios. Você pode inicializá-los e atualizá-los com os seguintes comandos:

```bash
cd kubernetes-labs
git submodule update --init --recursive
```

* `cd kubernetes-labs`: Navega para o diretório do repositório principal.
* `git submodule update`: Clona os submódulos nos seus respectivos diretórios.
* `--init`: Inicializa os submódulos, registrando-os no seu `.git/config`.
* `--recursive`: Garante que, se um submódulo tiver outros submódulos aninhados, eles também sejam inicializados e atualizados.

---

### 2. Atualizar Submódulos

À medida que o projeto avança, os submódulos podem ser atualizados no repositório principal. Para obter as últimas versões dos submódulos para as quais o `kubernetes-labs` aponta, execute:

```bash
cd kubernetes-labs
git submodule update --remote --merge
```

* `git submodule update`: Atualiza os submódulos.
* `--remote`: Faz com que cada submódulo seja atualizado para a ponta do branch remoto rastreado (geralmente `main` ou `master`), em vez do commit exato referenciado no repositório pai. **Use com cautela**, pois isso pode trazer commits mais recentes do que o projeto principal espera.
* `--merge`: Tenta mesclar as mudanças no submódulo, se houver commits locais.

**Recomendado para manter a sincronia com o repositório principal:**

Na maioria dos casos, especialmente ao sincronizar com as atualizações do time, o comando mais seguro e comum é simplesmente:

```bash
cd kubernetes-labs
git pull
git submodule update
```

* `git pull`: Puxa as últimas mudanças do repositório principal, incluindo quaisquer atualizações nas referências de commit dos submódulos.
* `git submodule update`: Atualiza os submódulos para os commits específicos que o repositório principal agora referencia.

---

### 3. Trabalhando Dentro de um Submódulo

Você pode navegar e trabalhar dentro de um submódulo como se fosse um repositório Git independente.

```bash
cd apps/kubernetes-labs-infra-demo
# Agora você está no diretório do submódulo kubernetes-labs-infra-demo
git status
git pull origin main # Ou qualquer branch que você queira
git checkout -b minha-nova-feature
# Faça suas alterações...
git add .
git commit -m "Minha nova feature no infra-demo"
git push origin minha-nova-feature
```

* Ao trabalhar dentro de um submódulo, você está em um repositório Git completamente funcional. Você pode criar branches, fazer commits e push como de costume.

**Importante:** Se você fizer commits dentro de um submódulo e quiser que o repositório principal reflita essa nova versão, você precisará comitar a mudança da referência do submódulo no repositório principal.

---

### 4. Enviando Mudanças no Submódulo para o Repositório Principal

Quando você faz alterações em um submódulo e as envia para o remoto do submódulo, o repositório principal ainda não sabe dessas alterações. Você precisa comitar a nova referência do submódulo no repositório principal:

```bash
# Primeiro, certifique-se de ter feito push das suas alterações no submódulo
cd apps/kubernetes-labs-infra-demo
git push origin minha-nova-feature # Exemplo
cd ../.. # Volta para o diretório raiz de kubernetes-labs

# Agora, comite a nova referência do submódulo no repositório principal
git add apps/kubernetes-labs-infra-demo
git commit -m "Atualiza kubernetes-labs-infra-demo para a nova feature"
git push origin main # Ou o branch principal do kubernetes-labs
```

* `git add apps/kubernetes-labs-infra-demo`: Adiciona a mudança na referência do submódulo ao índice do repositório principal. O Git reconhece que o SHA-1 do submódulo mudou.
* `git commit -m "..."`: Comita essa nova referência.
* `git push origin main`: Envia a mudança do repositório principal para o remoto.

---

### 5. Clonar e Trazer Todas as Branches de um Submódulo

Se você precisar inspecionar ou trabalhar em qualquer branch de um submódulo, você pode fazer isso depois de clonar o repositório principal.

```bash
# 1. Navegue para o diretório do submódulo
cd apps/kubernetes-labs-infra-cluster

# 2. Busque todas as branches do repositório remoto do submódulo
git fetch origin

# 3. Liste todas as branches disponíveis (locais e remotas)
git branch -a

# 4. Faça checkout de uma branch específica (exemplo: 'dev')
git checkout dev
# Se 'dev' for uma branch remota e você quiser criar uma local com tracking:
# git checkout -b dev origin/dev
```

* `git fetch origin`: Baixa todas as referências de branches e tags do repositório remoto do submódulo (`origin`), tornando-as visíveis localmente.
* `git branch -a`: Mostra todas as branches, incluindo as remotas (prefixadas com `remotes/origin/`).
* `git checkout [branch-name]`: Muda para a branch especificada.

---

## Considerações Finais

* **Sincronia:** Lembre-se que o repositório principal aponta para um commit específico de cada submódulo. Se você fizer alterações em um submódulo e não atualizar a referência no repositório principal, outros desenvolvedores que clonarem ou atualizarem o `kubernetes-labs` não verão suas mudanças no submódulo até que você comite a nova referência no repositório principal.

* **Detached HEAD:** Ao dar `checkout` em um commit específico ou em uma branch remota diretamente dentro de um submódulo (sem criar uma branch local de tracking), você estará em um estado de "detached HEAD". Isso significa que seu `HEAD` aponta diretamente para um commit, não para uma branch. É bom para inspeção, mas se você fizer commits nesse estado, eles não estarão associados a uma branch e podem ser perdidos se você mudar de branch.

Esperamos que este guia ajude você a navegar e trabalhar com os submódulos neste projeto! Se tiver dúvidas, não hesite em perguntar.

**Gerado com 🤖 AI**