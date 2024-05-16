# nome : Pedro lucas
sobre :
  fluxo de trabalho_dispatch :
  empurrar :
    galhos :
      - principal
permissões :
  conteúdo : leia
  páginas : escrever
  id-token : escrever
  
simultaneidade :
  grupo : " páginas "
  cancelamento em andamento : verdadeiro
empregos :
  construir :
    executado : ubuntu-mais recente
    passos :
    - nome : 📂 finalização da compra
      usa : ações/checkout@v4
    - nome : 💎 configurar Ruby
      usos : ruby/setup-ruby@250fcd6a742febb1123a77a841497ccaa8b9e939 # v1.152.0
      com :
        cache do bundler : verdadeiro
        versão do cache : 0

    - nome : 📄 páginas de configuração
      id : páginas
      usa : ações/configure-pages@ v4
      usa : ações/configure-pages@ v5

    - nome : 🔨 instalar dependências e construir site
      usos : actions/jekyll-build-pages@v1.0.12
      
    - nome : ⚡️ upload de artefato
      usa : ações/upload-pages-artifact@v3
  implantar :
    necessidades : construir
    ambiente :
      nome : páginas do github
      URL : ${{steps.deployment.outputs.page_url}}
    executado : ubuntu-mais recente
    passos :
      - nome : 🚀 implantar
        id : implantação
        usa : ações/deploy-pages@v4.0.5
