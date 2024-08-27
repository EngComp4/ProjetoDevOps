# Estrutura de Branches

## main
A `main` é a branch principal, contendo o código pronto para produção. **Protegida contra commits diretos**. Apenas código revisado e aprovado em uma branch de `release` é integrado à `main`. O deploy para produção é automatizado via CI/CD após a aprovação.

## develop
A `develop` é a branch de integração contínua, usada para testes e homologação de novas funcionalidades. **Protegida contra commits diretos**. Todas as mudanças passam por revisão e testes automáticos antes de serem integradas. Isso garante que o código na `main` esteja sempre em um estado de alta qualidade.

## release/x.x.x
Quando a `develop` está pronta para uma nova versão, uma branch `release/x.x.x` é criada. Aqui, realizamos os últimos ajustes antes de lançar a versão. Rebases frequentes da `develop` ajudam a manter a `release/x.x.x` atualizada e minimizam conflitos ao integrar de volta.

## release/x.x.x_nome_dev
Cada desenvolvedor trabalha em sua própria branch `release/x.x.x_nome_dev`, derivada da `release/x.x.x`. Isso permite o desenvolvimento isolado de tarefas. Após a conclusão, o desenvolvedor marca o último commit com uma tag e faz um cherry-pick para a branch `release/x.x.x`.

# Fluxo de Trabalho

### Criando uma Release
Quando a `develop` está pronta para a próxima versão, criamos uma branch `release/x.x.x` para preparar o lançamento, permitindo ajustes finais antes de ir para produção.

### Desenvolvendo nas Branches Individuais
Cada desenvolvedor cria sua branch a partir da `release/x.x.x` para trabalhar em suas tarefas, mantendo o desenvolvimento organizado e isolado.

### Evitando Conflitos entre develop e release/x.x.x
Como a `develop` pode continuar recebendo mudanças enquanto a `release/x.x.x` está em desenvolvimento, rebases frequentes da `release/x.x.x` na `develop` mantêm as branches sincronizadas, evitando conflitos na hora de integrar.

### Integrando e Finalizando
Após revisão e aprovação, a `release/x.x.x` é integrada primeiro na `develop` e depois na `main`, com revisões e testes automáticos garantindo a qualidade antes do lançamento em produção.

### O Que Acontece com as Branches Antigas
Após o lançamento, as branches de desenvolvimento individuais (`release/x.x.x_nome_dev`) são arquivadas. Elas permanecem disponíveis para consulta futura, sem impactar o histórico principal do projeto.

# Proteção e Automação

- As branches `main` e `develop` são protegidas, e qualquer mudança precisa passar por revisão e testes automáticos via CI/CD.
- O pipeline de CI/CD na `develop` executa todos os testes e verificações automáticas, enquanto na `main`, o CI/CD automatiza o deploy para produção assim que tudo estiver aprovado.
