<h1 align="center" style="font-weight: bold;">Código limpo: Habilidades Práticas de Agile Software</h1>

<div align="center">
  
<img src="https://m.media-amazon.com/images/I/51E2055ZGUL._AC_UF1000,1000_QL80_.jpg">

[Link](https://www.amazon.com.br/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882) para acessar o livro

---

</div>
<h3 align="left">Sumário 📄</h3>
<p align="left">
  <a href="#descricao">1. Descrição 📝</a><br>
  <a href="#descricao">2. Código Limpo</a><br>
  <a href="#descricao">3. Nomes Significativos</a><br>
  <a href="#descricao">4. Funções</a><br>
  <a href="#descricao">5. Comentários</a><br>
  <a href="#descricao">6. Formatação</a><br>
  <a href="#descricao">7. Objetos e Estruturas de Dados</a><br>
  <a href="#descricao">8. Tratamento de Erro</a><br>
  <a href="#descricao">9. Limites</a><br>
  <a href="#descricao">10. Testes de Unidade</a><br>
  <a href="#descricao">11. Classes</a><br>
  <a href="#descricao">12. Sistemas</a><br>
</p>

---

<h2 id="descricao"> 2. Código Limpo</h2>

Não basta apenas escrever um código que funcione; é essencial mantê-lo limpo e organizado. Com o tempo, códigos podem se degradar se não cuidarmos deles ativamente. Uma regra simples da organização de escoteiros dos EUA nos ensina a deixar o acampamento mais limpo do que quando o encontramos, e podemos aplicar essa ideia ao nosso trabalho: sempre deixe o código melhor do que o encontrou. Pequenas melhorias, como renomear variáveis para torná-las mais claras ou simplificar funções, podem prevenir a deterioração do código. Imagine trabalhar em um projeto onde o código melhora continuamente. Isso não é parte do profissionalismo?

---

<h2 id="descricao"> 3. Nomes Significativos</h2>

Um nome deve indicar claramente por que algo existe, o que faz e como é usado. Se um nome precisa de um comentário para ser entendido, ele não é bom o suficiente.

Em um código que manipula uma lista, usar nomes mais descritivos, como `gameBoard` para uma lista de células em um jogo de campo minado, e `getFlaggedCells()` para uma função que retorna células marcadas, torna o código muito mais compreensível. No final, escolher bons nomes torna o código mais explícito e fácil de entender, sem alterar sua complexidade.

Evitar informações erradas em nomes de variáveis, funções e classes é essencial para manter o código claro. Nomes devem refletir seu propósito real, evitando confusões e interpretações erradas. Evite nomes semelhantes ou visivelmente parecidos, como l e 1, pois podem causar erros. Nomes devem ter significados distintos, e palavras comuns ou redundantes devem ser evitadas. A clareza nos nomes facilita a compreensão do código e previne mal-entendidos.

Use nomes que sejam fáceis de buscar no código. Nomes de uma só letra ou números são difíceis de localizar e podem levar a erros, especialmente quando números grandes são usados incorretamente. Prefira nomes descritivos e longos quando necessário, para facilitar a busca e o entendimento do código. Variáveis com nomes curtos devem ser usadas apenas em escopos pequenos.

---

**3.1 Interfaces e Implementações:**

Ao nomear interfaces e implementações, evite codificações desnecessárias, como prefixar interfaces com "I". Prefira nomear a interface como `ShapeFactory` e, se necessário, adicione uma distinção na implementação, como ShapeFactoryImp. Isso mantém o código mais limpo e fácil de entender, evitando distrações e informações excessivas.

---

**3.2 Classes:**

Para nomes de classes, utilize substantivos como `Customer` ou `Account`. Evite termos genéricos como `Gerente` ou `Processador`, e nunca use verbos para nomear classes. Já os métodos devem ser nomeados com verbos que descrevam a ação que executam, como `save`, `delete`, ou `getName`.

---

**3.3 Métodos:**

Use verbos que descrevam claramente a ação que a função realiza. Métodos de acesso, modificação e verificação devem seguir um padrão semelhante ao de outras linguagens, como `get`, `set`, ou `is`.

---

**3.4 Contextos:**

Para tornar os nomes mais significativos, é importante garantir que eles estejam dentro de um contexto claro. Muitas vezes, nomes isolados podem perder o significado, especialmente se forem usados fora de seu contexto original. Uma forma de resolver isso é organizá-los dentro de classes, funções, ou namespaces que descrevam o contexto ao qual pertencem.

Por exemplo, variáveis como firstName, lastName, street, houseNumber, city, state, e zipcode. Quando vistas juntas, é evidente que formam um endereço. Porém, se você encontrar apenas a variável state em um método isolado, pode não ser claro que ela faz parte de um endereço.

```javascript
class Address {
    constructor(firstName, lastName, street, houseNumber, city, state, zipcode) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.street = street;
        this.houseNumber = houseNumber;
        this.city = city;
        this.state = state;
        this.zipcode = zipcode;
    }
}

let address = new Address("John", "Doe", "Main St", "123", "Springfield", "IL", "62701");
console.log(address.state);
```

Agora as variáveis state, city, etc., agora fazem parte de um contexto claro `(Address)`, o que elimina a necessidade de prefixos adicionais e melhora a clareza do código.

Evite adicionar contextos desnecessários aos nomes no seu código. Por exemplo, em um aplicativo fictício chamado "Gas Station Deluxe" (GSD), adicionar o prefixo GSD a todas as classes, como `GSDAccountAddress`, é redundante e pode atrapalhar mais do que ajudar. Isso pode fazer com que a lista de sugestões de autocompletar na IDE fique cheia de nomes longos e repetitivos, dificultando a navegação.

---

<h2 id="descricao"> 4. Funções</h2>

Funções devem ser pequenas e focadas em fazer apenas uma coisa, mantendo a clareza e facilitando a manutenção. Idealmente, devem ter poucos parâmetros, preferencialmente zero, e evitar a complexidade de múltiplos níveis de abstração. Usar nomes descritivos ajuda a entender o código sem necessidade de comentários adicionais.

Funções com um ou dois parâmetros são aceitáveis, mas, quando há mais, recomenda-se encapsulá-los em objetos. Evitar booleanos como parâmetros também é importante, pois indica que a função está fazendo mais de uma tarefa. Se necessário passar um número variável de parâmetros, listas ou varargs são preferíveis.

Estruturas como switch devem ser usadas com cautela e encapsuladas em classes, enquanto blocos try/catch devem ser extraídos para manter a lógica clara. Efeitos colaterais, como modificar estados externos, devem ser evitados. Exceções são preferíveis a códigos de erro, separando o fluxo de tratamento de erros da lógica principal.

---

<h2 id="descricao"> 5. Comentários</h2>

Comentários são uma forma de compensar a falta de clareza no código. No entanto, idealmente, o código deve ser tão claro que comentários se tornem desnecessários. Comentários podem se tornar desatualizados e enganosos, enquanto o código em si é a fonte mais confiável de verdade sobre o que o software faz.

Comentários muitas vezes são usados para explicar código confuso ou mal estruturado. Em vez de adicionar um comentário, é melhor refatorar o código para que ele seja autoexplicativo.

Comentários que fornecem informações básicas podem ser úteis, mas muitas vezes podem ser substituídos por bons nomes de funções ou variáveis. Exemplo:

```javascript
// Retorna uma instância do Responder sendo testado
function getResponderInstance() {
}
```

Como melhorar:

```javascript
function getResponderBeingTested() {
}
```

---

Às vezes, comentários são necessários para alertar sobre consequências específicas de uma função ou bloco de código. Esse tipo de comentário avisa aos desenvolvedores sobre potenciais problemas, como a longa duração de um teste.

Comentários `TODO` são úteis para marcar partes do código que precisam ser revisadas ou completadas no futuro. Esses comentários indicam claramente que algo precisa ser feito, e as IDEs modernas podem rastrear esses TODOs para garantir que não sejam esquecidos.

Use comentários para destacar a importância de certos detalhes que podem parecer triviais, mas são cruciais para o funcionamento correto do código. Exemplo:

```javascript
const listItemContent = match[3].trim();
// A função trim é importante. Remove espaços
// que poderiam causar problemas no reconhecimento do item como outra lista.
new ListItemWidget(this, listItemContent, this.level + 1);
```

---

Quando você se depara com a necessidade de adicionar um comentário explicativo em seu código, considere primeiro se é possível substituir o comentário por uma função ou variável bem nomeada. Isso não apenas elimina a necessidade do comentário, mas também melhora a clareza e a legibilidade do código.

---

<h2 id="descricao"> 6. Formatação </h2>

A formatação do código é um aspecto crucial para transmitir profissionalismo e atenção aos detalhes. Um código bem formatado não só facilita a leitura e manutenção, mas também reflete a disciplina e o cuidado dos desenvolvedores.

Não há um tamanho ideal absoluto, mas arquivos menores tendem a ser mais fáceis de gerenciar e compreender. Em JavaScript, isso pode significar dividir grandes módulos em arquivos menores e mais focados, cada um responsável por uma única responsabilidade ou funcionalidade. Use quebras de linha para dividir logicamente diferentes seções de código, como separando funções, classes ou blocos de código relacionados. Isso ajuda a evitar que o código pareça um bloco monolítico e facilita a navegação.

---

<h2 id="descricao"> 7. Objetos e Estruturas de Dados </h2>

Objetos expõem as ações e ocultam os dados, o que facilita a adição de novos tipos de objetos sem precisar modificar as ações existentes, mas torna mais difícil a inclusão de novas atividades em objetos já existentes. Por outro lado, estruturas de dados expõem os dados e não possuem ações significativas, facilitando a adição de novas ações às estruturas de dados existentes, mas dificultando a inclusão de novas estruturas de dados em funções existentes.

Em um sistema, a escolha entre objetos e estruturas de dados depende da flexibilidade desejada. Quando se busca flexibilidade para adicionar novos tipos de dados, a opção por objetos é mais adequada. Quando a necessidade é adicionar novas ações, optar por tipos de dados e procedimentos faz mais sentido.

Utilizar getters e setters em objetos é uma prática recomendada porque oferece várias vantagens, como facilitar a modificação do comportamento dos acessos aos dados sem alterar os pontos de chamada no código, permite adicionar validações ao definir valores (set), por encapsular a representação interna dos dados promove maior flexibilidade, e torna mais fácil adicionar logs e tratamentos de erros.

Exemplo ruim:
```javascript
function createProduct() {
  return {
    stock: 0, // Propriedade pública
  };
}

const product = createProduct();
product.stock = 50; // Modificação direta
```

Jeito correto segundo clean code:
```javascript
function createProduct() {
  // Propriedade privada
  let stock = 0;

  // Getter para acessar o estoque
  function getStock() {
    return stock;
  }

  // Setter para modificar o estoque, com validação
  function setStock(quantity) {
    if (quantity < 0) {
      throw new Error("A quantidade de estoque não pode ser negativa");
    }
    stock = quantity;
  }

  return {
    getStock,
    setStock,
  };
}

const product = createProduct();
product.setStock(50); // Modificação controlada
console.log(product.getStock()); // Acesso controlado
```

---

<h2 id="descricao"> 8. Tratamento de Erro </h2>

No passado, quando as linguagens de programação não suportavam exceções, era comum utilizar flags ou códigos de erro para indicar problemas, o que obrigava o chamador a verificar esses erros após cada chamada. Esse método resultava em código confuso e propenso a erros, já que os programadores podiam facilmente esquecer de verificar os erros.

**Exemplo sem Exceções:**

```javascript
function sendShutDown() {
    const handle = getHandle(DEV1);
    if (handle !== INVALID_HANDLE) {
        const record = retrieveDeviceRecord(handle);
        if (record.status !== DEVICE_SUSPENDED) {
            pauseDevice(handle);
            clearDeviceWorkQueue(handle);
            closeDevice(handle);
        } else {
            console.log("Device suspended. Unable to shut down");
        }
    } else {
        console.log("Invalid handle for:", DEV1);
    }
}
```

**Exemplo com Exceções:**

```javascript
function sendShutDown() {
    try {
        tryToShutDown();
    } catch (error) {
        console.error(error.message);
    }
}

function tryToShutDown() {
    const handle = getHandle(DEV1);
    if (handle === INVALID_HANDLE) {
        throw new Error("Invalid handle for: " + DEV1);
    }

    const record = retrieveDeviceRecord(handle);
    if (record.status === DEVICE_SUSPENDED) {
        throw new Error("Device suspended. Unable to shut down");
    }

    pauseDevice(handle);
    clearDeviceWorkQueue(handle);
    closeDevice(handle);
}
```

Nesse exemplo, o código principal (tryToShutDown) é separado do tratamento de erros (catch), tornando a lógica mais clara e o código mais fácil de manter.

---

Retornar null de funções ou passar null como argumento é uma prática que deve ser evitada, pois isso pode levar a erros em tempo de execução, como NullPointerException. Em vez de retornar null, é melhor lançar uma exceção ou usar um padrão de caso especial que retorne um objeto com um comportamento padrão.

```javascript
function registerItem(item) {
    if (item !== null) {
        const registry = persistentStore.getItemRegistry();
        if (registry !== null) {
            const existing = registry.getItem(item.getID());
            if (existing.getBillingPeriod().hasRetailOwner()) {
                existing.register(item);
            }
        }
    }
}

```

Esse código é propenso a erros porque depende de várias verificações de null.

**Refatoração com Objetos de Caso Especial:**

```javascript
function getItemRegistry() {
    return persistentStore.getItemRegistry() || new NullRegistry();
}

function getItem(itemID) {
    return registry.getItem(itemID) || new NullItem();
}
```

Agora, getItemRegistry e getItem sempre retornam um objeto válido, eliminando a necessidade de verificações de null.

Evitar também passar null para funções é ainda mais importante. Se uma função depende de argumentos não nulos, considere usar uma exceção ou validação antecipada.

---

<h2 id="descricao"> 9. Limites </h2>

Quando usamos bibliotecas de terceiros, é essencial entender como elas funcionam e como podemos integrá-las de forma eficaz ao nosso código. Em vez de apenas ler a documentação ou tentar integrar o código diretamente, podemos criar "testes de aprendizagem" para explorar o comportamento dessas APIs e entender melhor como elas funcionam.

**Exemplo de Teste de Aprendizagem:**

Suponha que queremos usar a biblioteca winston para logging. Podemos começar criando um teste simples para verificar se a configuração básica funciona conforme esperado.

**Teste Inicial:**

```javascript
const winston = require('winston');

// Teste simples para verificar o funcionamento básico do logger
function testLogCreate() {
    const logger = winston.createLogger({
        level: 'info',
        transports: [
            new winston.transports.Console()
        ]
    });

    logger.info('hello');
}

testLogCreate();

```

Após verificar que o logger básico funciona, podemos testar outras configurações, como formatos personalizados de saída:

```javascript
function testLogWithCustomFormat() {
    const logger = winston.createLogger({
        level: 'info',
        format: winston.format.combine(
            winston.format.colorize(),
            winston.format.timestamp(),
            winston.format.printf(({ timestamp, level, message }) => {
                return `${timestamp} ${level}: ${message}`;
            })
        ),
        transports: [
            new winston.transports.Console()
        ]
    });

    logger.info('hello with custom format');
}

testLogWithCustomFormat();
```

Depois de explorar e aprender como a biblioteca funciona, podemos encapsular esse conhecimento em uma função ou classe para uso em toda a aplicação, mantendo a lógica de configuração separada e reutilizável:

```javascript
function createLogger() {
    return winston.createLogger({
        level: 'info',
        format: winston.format.combine(
            winston.format.colorize(),
            winston.format.timestamp(),
            winston.format.printf(({ timestamp, level, message }) => {
                return `${timestamp} ${level}: ${message}`;
            })
        ),
        transports: [
            new winston.transports.Console()
        ]
    });
}

const logger = createLogger();
logger.info('Logger is ready to use across the application.');
```

---

<h2 id="descricao"> 10. Testes de Unidade </h2>

Os testes de unidade bem escritos e mantidos são a chave para manter o código de produção flexível e fácil de modificar. Testes robustos permitem que os desenvolvedores façam alterações no código com confiança, sabendo que qualquer erro será rapidamente detectado. Isso, por sua vez, facilita a manutenção da arquitetura do código e permite melhorias contínuas.

A qualidade mais importante em um teste é a legibilidade. Testes legíveis são claros, simples e consistentes, facilitando a compreensão e a manutenção. A clareza e a simplicidade nos testes permitem que eles transmitam seu propósito de forma direta, sem sobrecarregar o leitor com detalhes desnecessários.

Considere testes que têm código duplicado ou excesso de detalhes que obscurecem o objetivo do teste. Um exemplo típico seria testes com muitas chamadas repetidas ou detalhes que não contribuem para a compreensão do teste. Refatorar esses testes para eliminar duplicação e tornar a intenção mais clara é essencial para manter a qualidade.

---

Os testes limpos seguem cinco princípios essenciais:

- Rápidos (Fast): Devem ser rápidos para incentivar execuções frequentes e detecção precoce de problemas.

- Independentes (Independent): Devem rodar de forma independente, sem depender de outros testes.

- Repetíveis (Repeatable): Precisam ser repetíveis em qualquer ambiente, garantindo consistência nos resultados.

- Autovalidados (Self-Validating): Devem retornar um resultado claro (passou/falhou) sem necessidade de verificação manual.

- Pontuais (Timely): Devem ser escritos no momento certo, de preferência antes do código de produção, para garantir testabilidade.

---

<h2 id="descricao"> 11. Classes </h2>

As classes devem ser pequenas e focadas em uma única responsabilidade, seguindo o Princípio da Responsabilidade Única (SRP). Isso significa que uma classe deve ter apenas um motivo para mudar, e se houver múltiplas razões para alteração, deve-se considerar dividir a classe. Por exemplo, métodos que lidam com diferentes aspectos de um sistema podem ser extraídos em classes menores e mais específicas, assim como no exemplo da SuperDashboard e a extração de responsabilidades relacionadas à versão para uma nova classe.

Na organização das classes em JavaScript, as variáveis privadas (usando o # para encapsulamento) devem ser declaradas no início, seguidas de métodos públicos e privados. Métodos que fazem parte de um comportamento comum devem ser colocados próximos uns dos outros, de modo que o código seja lido de cima para baixo, mantendo uma organização lógica e facilitando a leitura.

A coesão também é essencial. Cada método de uma classe deve manipular uma ou mais variáveis da instância. Quando os métodos compartilham muitas variáveis, isso sugere que a classe é coesa. Porém, se as variáveis e métodos se tornam independentes entre si, a classe perde coesão e deve ser dividida. Um exemplo seria uma classe Stack, onde todos os métodos manipulam diretamente as variáveis de instância, garantindo coesão.

Para manter o código mais isolado de alterações, o uso de interfaces ou classes abstratas (em JavaScript, interfaces podem ser simuladas com classes ou tipos) pode ajudar a separar o comportamento de detalhes de implementação. Isso evita que mudanças em detalhes concretos afetem outras partes do sistema.

---

<h2 id="descricao"> 12. Sistemas </h2>

> "Complexidade mata. Ela suga a vida dos desenvolvedores, dificulta o planejamento, a construção e o teste dos produtos”.
> —Ray Ozzie, CTO, Microsoft Corporation

Assim como na analogia de construir uma cidade, onde diferentes equipes gerenciam partes específicas, em software, devemos dividir responsabilidades entre diferentes módulos e classes. Essa abordagem modular facilita o desenvolvimento, manutenção e crescimento do sistema.

Em JavaScript, é importante separar a construção dos objetos e o uso do sistema. Uma boa prática é mover a inicialização e configuração de dependências para uma camada externa, geralmente o arquivo principal (main) ou uma função de inicialização. Esse arquivo é responsável por instanciar objetos e passar dependências para o restante do sistema, mantendo o código de lógica de negócios separado da lógica de inicialização.

Um exemplo seria usar um factory para criar objetos, em vez de instanciá-los diretamente no código principal. Isso mantém o sistema desacoplado dos detalhes de implementação da construção dos objetos, permitindo mais flexibilidade. Exemplo:

```javascript
class LineItem {
  constructor(product, quantity) {
    this.product = product;
    this.quantity = quantity;
  }
}

class Order {
  constructor() {
    this.items = [];
  }

  addItem(item) {
    this.items.push(item);
  }
}

class LineItemFactory {
  create(product, quantity) {
    return new LineItem(product, quantity);
  }
}

// No main, fazemos a separação
const factory = new LineItemFactory();
const order = new Order();
order.addItem(factory.create('Product A', 10));
```

Nesse exemplo, a responsabilidade de criar LineItem foi movida para LineItemFactory, separando a lógica de criação da lógica de uso no Order.

---

A Injeção de Dependência (DI) é uma técnica poderosa para desacoplar dependências. Em JavaScript, frameworks como NestJS e InversifyJS suportam DI nativamente, mas também podemos implementá-la manualmente. O DI permite que as dependências sejam passadas para uma classe por meio de seu construtor ou setters, em vez de serem criadas dentro da própria classe, promovendo flexibilidade e testabilidade.

Sistemas podem começar simples e crescer conforme as necessidades mudam. No início, podemos adotar uma arquitetura mínima e aumentar a complexidade conforme a demanda cresce. Essa prática segue a filosofia ágil de desenvolver **iterativamente**, refatorando e melhorando o sistema à medida que novas funcionalidades são adicionadas. O objetivo é implementar apenas o que é necessário hoje, sabendo que refatorações farão parte do processo de crescimento.

Padrões como Factory e Dependency Injection são amplamente usados porque facilitam a reutilização e a manutenção do código. No entanto, é importante usá-los quando trazem valor real ao projeto. Não devemos adotar padrões complexos apenas por serem populares, mas sim quando eles simplificam a implementação ou oferecem vantagens claras para o sistema.

---