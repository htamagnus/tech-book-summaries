<h1 align="center" style="font-weight: bold;">Desconstruindo a Web: As tecnologias por trás de uma requisição 🔍</h1>

<div align="center">
  
<img src="https://m.media-amazon.com/images/I/410bCUoATQL.jpg">

[Link](https://www.casadocodigo.com.br/products/livro-desconstruindo-web) para acessar o livro

</br>

---

</div>
<h3 align="left">Sumário 📄</h3>
<p align="left">
  <a href="#descricao">1. Descrição 📝</a><br>
  <a href="#navegador">2. Navegador 🌐</a><br>
  <a href="#so">3. Sistema Operacional e Resolução de nomes 🖥️</a><br>
  <a href="#redes">4. Resolução de nomes na rede 🌐</a><br>
  <a href="#hypertexto">5. Transferindo hypertexto 📄➡️📄</a><br>
  <a href="#https">6. HTTPS e sua segurança 🔒</a><br>
  <a href="#internet">7. Internet 🌎</a><br>
  <a href="#servidor">8. Servidor Web 🖥️</a><br>
  <a href="#framework">9. O framework e a aplicação 🛠️</a><br>
  <a href="#devolta">10. De volta ao navegador 🔄🌐</a><br>
  <a href="#resumao">11. Resumão 📚✨</a><br>
</p>

---

<h2 id="descricao"> Descrição 📝</h2>

Esse é um resumo pessoal do livro [Desconstruindo a web](https://www.casadocodigo.com.br/products/livro-desconstruindo-web): as tecnologias por trás de uma requisição, da Casa do Código. Para o estudo desse livro, o autor se baseou no navegador chromium e na linguagem Ruby. Como eu trabalho com Javascript, adicionei alguns detalhes em certos parágrafos para pensar em como seria se estivessemos lidando com Javascript ao invés de Ruby. 

No livro de Willian Molinari, é apresentado um estudo detalhado sobre o funcionamento de uma requisição web, desde o momento em que o usuário pressiona a tecla Enter até a página estar completamente carregada. Ele explora como o navegador cria a requisição HTTP ou HTTPS, como o sistema operacional monta os pacotes de dados, a transmissão desses pacotes pela rede, o estabelecimento de uma conexão segura via HTTPS, e o processamento da requisição no servidor de aplicação utilizando um framework de desenvolvimento web. Finalmente, descreve como a resposta é enviada de volta ao navegador para ser renderizada, utilizando uma página HTML como exemplo para ilustrar cada etapa desse processo.


<img src="https://images2.imgbox.com/2f/f4/RpIjA27L_o.png">


<h2 id="navegador"> Navegador 🌐</h2>

Para o estudo desse livro, o autor se baseou no **navegador chromium** e na linguagem **Ruby**. 
Quando usamos um navegador para acessar um site, um complexo processo ocorre nos bastidores para transformar o que digitamos na barra de endereços em uma página web funcional. Esse processo envolve a interpretação da entrada do usuário, a escolha do protocolo adequado, o gerenciamento do cache da URL e a resolução de nomes de domínio.

O navegador precisa primeiramente interpretar o que foi digitado na **barra de endereços**. Isso pode ser uma URL válida ou uma frase a ser pesquisada em um motor de busca. Quando o usuário digita uma [URI](https://woliveiras.com.br/posts/url-uri-qual-diferenca) (A URI une o Protocolo (https://) a localização do recurso (URL - woliveiras.com.br) e o nome do recurso), como "desconstruindoaweb.com.br", o navegador determina se deve tratá-la como uma URL direta ou uma consulta de busca.

Após entender o que foi digitado, o navegador seleciona o protocolo apropriado para acessar o conteúdo. Na ausência de um [cabeçalho HSTS](https://kinsta.com/pt/base-de-conhecimento/hsts-seguranca-restrita-transporte/) (HTTP Strict Transport Security), o navegador pode optar por utilizar HTTP ao invés de HTTPS, adicionando o protocolo necessário à URL.

<img src="https://kinsta.com/pt/wp-content/uploads/sites/3/2016/11/strict-transport-security-HTTP-response.png">

Com a URL completa, o navegador **verifica** se já possui o conteúdo em seu **cache local**. Se o cache for válido, o navegador serve o conteúdo diretamente a partir do cache. Caso contrário, ele inicia o processo de busca do conteúdo na internet. O navegador mantém um cache de URLs para acelerar o acesso a sites visitados anteriormente. Se a entrada do cache estiver válida, o navegador utilizará esses dados para carregar a página mais rapidamente, sem a necessidade de buscar o conteúdo novamente na internet. Para verificar se um cache é válido, o navegador pode comparar o tempo decorrido desde o acesso inicial com o valor de **max-age** no cabeçalho **Cache-Control** ou, na ausência desse cabeçalho, verificar se a data no cabeçalho Expires já passou em relação à data atual. Se o cache estiver expirado em ambos os casos, o conteúdo atualizado será buscado no servidor.

<img src="https://www.cloudflare.com/img/learning/cdn/glossary/what-is-cache-control/cache-control-header.png">

Para acessar um site na internet, é necessário conhecer o endereço IP associado ao nome do domínio. O navegador possui um sistema interno para resolução de nomes, que faz cache de informações de **DNS (Domain Name System)**. Se necessário, o navegador buscará essas informações na internet. No caso do Chromium, ele utiliza bibliotecas do sistema operacional para realizar a resolução de nomes.

---

<h2 id="so">Sistema Operacional e Resolução de nomes 🖥️</h2>

Após separar o **domínio da URI**, o navegador delega a resolução de nomes ao sistema operacional, que é definido pela plataforma em uso (Windows, macOS, Linux, etc.). No caso do Linux, a **biblioteca glibc** é utilizada para fazer chamadas de sistema. A função **getaddrinfo** da glibc resolve nomes consultando os registros de IPv4 e IPv6 no servidor DNS, permitindo a criação de uma conexão com o servidor de destino. O protocolo IP tem duas versões principais: IPv4, com endereços de 32 bits, e IPv6, com endereços de 128 bits. O navegador então utiliza o algoritmo Happy Eyeballs para preferir IPv6, sem comprometer a performance caso ele não esteja disponível.

<img src="https://blog.baehost.com/wp-content/uploads/2016/11/Happy-eyeballs-1.png">

O algoritmo **Happy Eyeballs** é projetado para melhorar a experiência do usuário na internet ao tentar conectar-se a um servidor que suporta tanto IPv4 quanto IPv6. Ele faz isso tentando estabelecer conexões em ambos os protocolos simultaneamente, preferindo IPv6 sempre que possível. Se a conexão IPv6 falhar ou demorar muito, a conexão IPv4 será usada para evitar atrasos.

---

<h2 id="redes">Resolução de nomes na rede 🌐</h2>

Uma requisição web passa por várias camadas do "modelo Ozzy", que simplifica as camadas do **modelo OSI** em cinco: aplicação, transporte, rede, enlace e física. O protocolo DNS está na camada de aplicação, sendo gerenciado por aplicações do usuário como o Chromium ou a glibc, não pelo kernel. Para resolver o domínio "desconstruindoaweb.com.br", procuramos entradas A do DNS que contêm o endereço IPv4 desejado.
<img src="https://blogs.manageengine.com/wp-content/uploads/2022/10/dns.png">

A **glibc**, utilizando pacotes UDP, cria um **socket** (uma abstração criada pelo sistema operacional para fazer a transferência de dados de um ponto a outro) com a syscall socket e o conecta com a **syscall connect**. O UDP, sendo não orientado à conexão, permite o envio de pacotes sem garantir a entrega ou ordem. O DNS consulta root servers, servidores de Top-Level Domain e finalmente o servidor autoritativo do domínio, que retorna o endereço IP.
<img src="https://files.tecnoblog.net/wp-content/uploads/2022/05/modelo-osi-1.png">

---

<h2 id="hypertexto">Transferindo hypertexto 📄➡️📄</h2>

O protocolo HTTP tem duas versões principais: **HTTP/2**, que traz várias inovações, e **HTTP/1.1**, amplamente utilizado e baseado em texto, podendo ser reproduzido com comandos como telnet. O método HTTP mais comum para solicitar uma página é o GET. Uma conexão HTTP/1.1 via telnet começa com o comando GET / HTTP/1.1, que requisita a raiz da aplicação. 
<img src="https://blog-static.infra.grancursosonline.com.br/wp-content/uploads/2023/02/22170807/Imagem4.artigo.22.02-300x177.png">

O HTTP opera sobre o TCP, que requer o **three-way handshake** antes de estabelecer a conexão. Esse processo inicial envolve três etapas: o cliente envia um SYN, o servidor responde com SYN-ACK, e o cliente finaliza com um ACK, estabelecendo a conexão para troca de dados.
<img src="https://miro.medium.com/v2/resize:fit:1400/0*abcrVbeLBaZaVqpk.jpg">

---

<h2 id="https">HTTPS e sua segurança 🔒</h2>

O HTTPS é a forma segura de transportar HTTP, utilizando o protocolo TLS para criptografar os dados. O processo começa com a resolução de domínio e o **three-way handshake do TCP**. Em seguida, ocorre o handshake do TLS, que começa com o "Client Hello" enviado pelo cliente ao servidor, indicando as opções de conexão. O servidor responde com "Server Hello", envia um certificado digital contendo uma chave pública e outros dados de verificação. Após a validação do certificado pelo cliente, é gerado um par de chaves para criptografia simétrica. Ambos os lados enviam "Change Cipher Spec", e toda a comunicação subsequente é criptografada. O HTTPS ganhou popularidade com a extensão [Firesheep](https://g1.globo.com/tecnologia/noticia/2010/11/programa-facilita-roubo-de-contas-de-sites-em-redes-sem-fio-publicas.html) para firefox, que mostrou a vulnerabilidade das conexões HTTP em texto puro.
<img src="https://www.stg.ssl.com/wp-content/uploads/2023/09/SSLTLS-Handshake-600x600.png">

---

<h2 id="internet">Internet 🌎</h2>

Chegou a hora de acessar a internet via **Wi-Fi**, utilizando uma placa da Intel com o driver **iwlwifi**. O sinal passa por várias partes do kernel, incluindo socket, af_inet, tcp, ip, driver da placa e firmware. A informação pode trafegar por redes públicas ou seguras configuradas com WPA2. O 4-way **handshake do WPA2**, realizado ao conectar à rede, garante a segurança dos dados transmitidos por ondas de rádio. A conexão atravessa interferências de dispositivos na mesma frequência até chegar ao roteador, que envia os pacotes para a internet, passando por vários saltos até alcançar o servidor de destino.

---

<h2 id="servidor">Servidor Web 🖥️</h2>

O servidor web pode ser tanto um computador físico num datacenter quanto um software que responde às requisições. Neste estudo, usamos o **NGINX** como software servidor. O NGINX usa um processo principal (master) e vários processos de trabalho (workers). Os workers lidam com as requisições de forma assíncrona, utilizando um sistema de eventos chamado epoll. Se a requisição não for por conteúdo estático, o NGINX age como um proxy reverso e se comunica com o servidor de aplicação através de um unix socket.

O servidor de aplicação que usamos é o **Phusion Passenger**, que recebe as requisições HTTP e interage com a aplicação. Para isso, adicionamos um módulo ao NGINX, que permite que ele se comunique com o Passenger. O Passenger então processa a requisição e retorna o resultado esperado.

<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT-vKaSU4nLUWnFREDkyiyVBXWlBmPjXxb3AQ&s">

---

<h2 id="framework">O framework e a aplicação 🛠️</h2>

O **Rack** é uma interface que conecta servidores de aplicação a frameworks web em Ruby, facilitando a comunicação entre eles. No nosso estudo, usamos o Passenger como servidor de aplicação, que carrega a aplicação em processos separados e cria clones para otimizar recursos. O Passenger utiliza threads para lidar com múltiplas requisições, comunicando-se com a aplicação através do Rack. O Rack, por sua vez, interage com o framework Ruby on Rails (Rails).

O Rails segue o **padrão MVC**, onde as requisições passam por middlewares do Rack, conectam-se ao sistema de rotas do Rails, executam métodos do controller e renderizam views com códigos Ruby. Após processar a requisição, a resposta retorna pelo mesmo caminho, passando pelos middlewares do Rack até chegar ao Passenger. O Passenger então transforma a resposta e a envia ao servidor web via unix socket.

O servidor web escreve a resposta no **socket do cliente**. A resposta percorre a camada Ozzy do servidor, sai pela placa de rede do datacenter, passa por dispositivos de rede até o roteador local, e é enviada via Wi-Fi ao computador do usuário. O sinal é processado pela camada Ozzy local, convertendo-se em um pacote HTTP que o navegador interpreta e exibe ao usuário.

<img src="https://miro.medium.com/v2/resize:fit:769/0*INnD9_mOgyxNsVIP.png">

## Mas e se fosse em Javascript?
Se fosse em JavaScript, o equivalente ao Rack seria o middleware **Express.js**, que é uma parte do Node.js. 

O **Express.js** é uma interface que conecta servidores de aplicação a frameworks web em JavaScript, facilitando a comunicação entre eles. No nosso estudo, se usássemos Node.js com Express.js como servidor de aplicação, ele gerenciaria as requisições de forma assíncrona e eficiente.

O **Express.js** segue um padrão semelhante ao MVC, onde as requisições passam por middlewares, conectam-se ao sistema de rotas, executam funções de controle e renderizam views com templates ou dados JSON. Após processar a requisição, a resposta retorna pelo mesmo caminho, passando pelos middlewares do Express.js até chegar ao cliente.

O servidor web então escreve a resposta no socket do cliente. A resposta percorre a camada de rede do servidor, sai pela placa de rede do datacenter, passa por dispositivos de rede até o roteador local, e é enviada via Wi-Fi ao computador do usuário. O sinal é processado pela camada de rede local, convertendo-se em um pacote HTTP que o navegador interpreta e exibe ao usuário.

---

<h2 id="devolta">De volta ao navegador 🔄🌐</h2>

Após enviar a requisição, o navegador recebe dados do site "desconstruindoaweb.com.br". Metadados como **ETag** e **Cache-Control** são extraídos dos cabeçalhos HTTP, junto com o corpo HTML. Essas informações são passadas para a engine de renderização Blink do Chromium, que começa a processar o HTML. 

**O parse do HTML** transforma o HTML em uma estrutura de árvore chamada DOM e o **parse do CSS** cria uma segunda árvore chamada CSSOM. O Render Tree combina DOM e CSSOM para criar a Render Tree, que contém os elementos a serem exibidos. O Layout define a posição exata de cada elemento na tela e o Paiting renderiza visualmente os elementos, mostrando o conteúdo ao usuário.
<img src="https://www.w3schools.com/js/pic_htmltree.gif">

## Mas e se fosse em React?
Se fosse em JavaScript usando um framework como **React**, o processo de renderização seria semelhante, mas com algumas diferenças específicas devido ao uso de uma biblioteca de interface de usuário. Após enviar a requisição, o navegador recebe os dados do site. Metadados como ETag e Cache-Control são extraídos dos cabeçalhos HTTP, junto com o corpo HTML e os arquivos JavaScript necessários. Essas informações são passadas para a engine de renderização Blink do Chromium. 

**O parse do HTML** transforma o HTML no DOM, e o parse do Javascript carrega e executa os scripts Javascript, incluindo React. O React cria uma representação virtual do DOM na memória chamada Virtual DOM, e o React compara o Virtual DOM com o DOM real e determina as mudanças necessárias. Com isso, são transformados e posicionados os componentes em elementos DOM. O navegador define a posição exata de cada elemento na tela (layout) e os renderiza visualmente (painting), exibindo o conteúdo ao usuário.

Em vez de processar HTML puro, React utiliza componentes que são funções ou classes retornando elementos React. Estes componentes são combinados para formar a interface do usuário. O React utiliza estado (state) e propriedades (props) para gerenciar e passar dados entre componentes. Quando o estado ou as propriedades mudam, React automaticamente re-renderiza os componentes afetados, atualizando a interface de usuário sem recarregar a página inteira.
<img src="https://media.geeksforgeeks.org/wp-content/uploads/20230725135348/Browser-DOM-Virtual-DOM-copy.webp">

---

<h2 id="resumao">Resumão 📚✨</h2>

<img src="https://images2.imgbox.com/2f/f4/RpIjA27L_o.png">

1. **Início da Requisição:** O usuário digita uma URL no navegador, que transforma a URI em uma URL completa e verifica o cache. Se não houver cache válido, o navegador resolve o domínio usando DNS e estabelece uma conexão TCP via three-way handshake.

2. **Conexão Segura (HTTPS):** Se a conexão for HTTPS, o navegador realiza o handshake TLS para criptografar a comunicação.

3. **Requisição e Resposta HTTP:** O navegador envia uma requisição HTTP ao servidor, que no nosso estudo é gerenciado pelo NGINX. O NGINX pode atuar como um proxy reverso e comunicar-se com o servidor de aplicação (Phusion Passenger) via unix socket. No caso de Javascript, aqui seria usado o Express.

4. **Processamento pelo Servidor de Aplicação:** O Phusion Passenger carrega a aplicação Ruby on Rails, utilizando o Rack para interface entre o servidor e a aplicação. O Rails processa a requisição, utilizando seu sistema MVC para gerar a resposta HTML.

5. **Envio da Resposta:** A resposta gerada pelo Rails é enviada de volta através do Passenger, NGINX e rede até o navegador do cliente.

6. **Recebimento e Renderização no Navegador:**

- **Recebimento dos Dados:** O navegador recebe os cabeçalhos HTTP e o corpo HTML.
- **Parsing:** O Blink, engine de renderização do Chromium, faz o parsing do HTML para criar o DOM e do CSS para criar o CSSOM.
- **Render Tree:** Combina DOM e CSSOM para criar a Render Tree.
- **Layout e Painting:** Define a posição dos elementos na tela (layout) e os renderiza visualmente (painting).
- **Interatividade (JavaScript/React):** Se a aplicação utiliza JavaScript ou frameworks como React, o navegador carrega e executa os scripts, utilizando o Virtual DOM para gerir atualizações e renderizar componentes de forma eficiente.

---
