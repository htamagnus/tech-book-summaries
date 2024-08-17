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

Nomes no código devem ser claros e significativos, refletindo seu propósito sem a necessidade de comentários. Bons nomes tornam o código mais fácil de entender e mantêm a complexidade baixa. Ao lidar com listas, por exemplo, prefira nomes descritivos como gameBoard para uma lista de células e getFlaggedCells() para uma função que retorna células marcadas.

Evite nomes que possam causar confusão ou contenham informações erradas, como variáveis ou classes com nomes semelhantes. Prefira nomes que sejam fáceis de buscar e usar no código, evitando nomes curtos e confusos, especialmente em escopos amplos. Exemplo:

```javascript
// Ruim:
setTimeout(blastOff, 86400000);

// Melhor:
const MILLISECONDS_PER_DAY = 86400000;
setTimeout(blastOff, MILLISECONDS_PER_DAY);
```

Para classes, use substantivos como Customer ou Account, enquanto métodos devem ser nomeados com verbos que descrevem suas ações, como save, delete, ou getName. Ao nomear interfaces e implementações, evite prefixos desnecessários como "I", e mantenha os nomes simples e descritivos. Exemplo:

```javascript
// Ruim:
class Processador {
  save() { /* ... */ }
}

// Melhor:
class UserAccount {
  save() { /* ... */ }
}
```

Contexto é essencial. Nomes devem ser claros dentro de seu escopo, como no exemplo de uma classe Address que agrupa variáveis relacionadas a um endereço. Evite prefixos redundantes que tornam o código prolixo e desnecessariamente longo. Prefira variáveis explicativas e substitua números "mágicos" por constantes com nomes significativos, como MILLISECONDS_PER_DAY em vez de 86400000. Exemplo:

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

const address = new Address("John", "Doe", "Main St", "123", "Springfield", "IL", "62701");
console.log(address.state);
```

Em loops e funções, use nomes descritivos para parâmetros, evitando mapeamentos mentais. Finalmente, ao invés de usar curto-circuito para definir valores padrões, utilize argumentos padrões em funções para garantir maior clareza.

---

<h2 id="descricao"> 4. Funções</h2>

Funções devem ser pequenas e realizar apenas uma tarefa, facilitando a compreensão e a manutenção. Elas devem ter poucos parâmetros, preferencialmente zero, e evitar múltiplos níveis de abstração. Nomes descritivos ajudam a entender o código sem precisar de comentários.

Limitar o número de parâmetros é crucial para facilitar o teste e evitar complexidade. Funções com mais de dois parâmetros devem preferir objetos ou usar desestruturação para melhorar a clareza.

Estruturas como switch devem ser usadas com cautela e encapsuladas em classes, enquanto blocos try/catch devem ser extraídos para manter a lógica clara. Efeitos colaterais, como modificar estados externos, devem ser evitados. Exceções são preferíveis a códigos de erro, separando o fluxo de tratamento de erros da lógica principal.

Em resumo as funções devem fazer apenas uma coisa, o nome deve descrever a ação, evitar efeitos colaterais e flags como parâmetro.

**Exemplo ruim:**
```javascript
function handleUserUpdate(user, updateType, isAdmin) {
  if (isAdmin) {
    if (updateType === 'password') {
      user.password = 'newPassword123';
      console.log(`Password updated for user: ${user.name}`);
    } else if (updateType === 'email') {
      user.email = 'newemail@example.com';
      console.log(`Email updated for user: ${user.name}`);
    }
  } else {
    console.log('User does not have admin privileges to update.');
  }

  if (updateType === 'notify') {
    console.log('Sending notification to user...');
    user.notifications.push('Notification sent!');
  }
}
```

**Problemas:** A função faz várias coisas (atualiza senha, email e notifica o usuário), usa isAdmin como flag, levando a múltiplos caminhos de código, tem efeitos colaterais (modifica diretamente o objeto user e seu estado), o código está duplicado na lógica de atualização e o nome não descreve claramente a ação da função.

---

**Exemplo correto segundo clean code:**
```javascript
function updateUserPassword(user, newPassword) {
  user.password = newPassword;
  logUpdate('Password', user);
}

function updateUserEmail(user, newEmail) {
  user.email = newEmail;
  logUpdate('Email', user);
}

function logUpdate(updateType, user) {
  console.log(`${updateType} updated for user: ${user.name}`);
}

function notifyUser(user) {
  console.log('Sending notification to user...');
  user.notifications = [...user.notifications, 'Notification sent!'];
}

function handleUserUpdate(user, updateType, isAdmin = false) {
  if (!isAdmin) {
    console.log('User does not have admin privileges to update.');
    return;
  }

  switch (updateType) {
    case 'password':
      updateUserPassword(user, 'newPassword123');
      break;
    case 'email':
      updateUserEmail(user, 'newemail@example.com');
      break;
    case 'notify':
      notifyUser(user);
      break;
    default:
      console.log('Invalid update type');
  }
}
```
**Melhorias:** faz apenas uma coisa por função, o nome está descritivo, sem efeitos colaterais, sem flags desnecessárias e o código duplicado foi removido.

---

<h2 id="descricao"> 5. Comentários</h2>

Comentários devem ser evitados sempre que o código puder ser autoexplicativo. Refatorar o código para torná-lo claro é preferível a adicionar comentários explicativos. Nomes descritivos para funções, variáveis e classes podem substituir a maioria dos comentários, tornando o código mais legível e menos propenso a se tornar desatualizado.

Comentários só são úteis em casos de lógica de negócio complexa ou para alertar sobre algo específico e potencialmente problemático. Comentários como TODO podem ser usados para marcar áreas que precisam de atenção futura.

Evite manter código comentado na base de código e não registre alterações diretamente nos comentários, pois o controle de versão já lida com isso. Não use marcadores de posição, como linhas de divisão, para separar seções do código.

**Exemplo ruim:**

```javascript
function calculateHash(data) {
  // Cria uma hash
  let hash = 0;

  // Comprimento da string
  const length = data.length;

  // Loop em cada caractere
  for (let i = 0; i < length; i++) {
    // Pega o código do caractere
    const char = data.charCodeAt(i);
    // Gera a hash
    hash = ((hash << 5) - hash) + char;
    // Converte para inteiro 32-bit
    hash &= hash;
  }

  // TODO: adicionar suporte a outras codificações
  return hash;
}

// doSomeWork();
// doOtherStuff();  // código desnecessário comentado

/**
 * 2023-08-17: Adicionada função de hash (TS)
 * 2023-07-22: Melhorada função de hash (JP)
 */
function combine(a, b) {
  return a + b;
}

////////////////////////////////////////////////////////////////////////////////
// Configuração inicial do sistema
////////////////////////////////////////////////////////////////////////////////
const config = {
  retries: 5,
  timeout: 2000
};
```
**Problemas:** comentários explicando o óbvio (como "Cria uma hash"), código comentado deixado na base de código, registro de alterações desnecessário e marcadores de posição sem valor real


---

**Exemplo correto segundo clean code:**
```javascript
function calculateHash(data) {
  let hash = 0;
  const length = data.length;

  for (let i = 0; i < length; i++) {
    const char = data.charCodeAt(i);
    hash = ((hash << 5) - hash) + char;
    hash &= hash;  // Converte para 32-bit
  }

  return hash;
}

function combine(a, b) {
  return a + b;
}

const config = {
  retries: 5,
  timeout: 2000
};
```

**Melhorias:** sem comentários desnecessários, remoção do código comentado, sem registros de alterações no código e eliminação de mercadores de posição.

---

<h2 id="descricao"> 6. Formatação </h2>

A formatação é essencial para garantir um código legível e profissional. Um código bem formatado facilita a leitura, a manutenção e reflete o cuidado do desenvolvedor. Arquivos menores, bem divididos, são mais fáceis de gerenciar. Ferramentas automáticas de formatação, como linters e formatadores, são recomendadas para evitar discussões desnecessárias sobre estilo.

Seja consistente com a capitalização em variáveis, funções e classes. Funções e chamadas de funções devem estar próximas verticalmente para facilitar a leitura, respeitando o fluxo natural de leitura de cima para baixo.

**Exemplo ruim:**

```javascript
const ITEMS_IN_CART = 3;
const items_in_stock = 50;

const products = ['Laptop', 'Smartphone', 'Headphones'];
const Categories = ['Electronics', 'Accessories', 'Home Appliances'];

function place_order() {}
function cancel_order() {}

class user {}
class Order {}

class OrderManager {
  constructor(order) {
    this.order = order;
  }

  checkStock() {
    return db.lookup(this.order, 'stock');
  }

  getOrderDetails() {
    const stock = this.checkStock();
    // ...
  }

  processOrder() {
    this.getOrderDetails();
    this.sendInvoice();
    this.updateStock();
  }

  sendInvoice() {
    // ...
  }

  updateStock() {
    const stock = this.checkStock();
  }
}

const orderManager = new OrderManager(order);
orderManager.processOrder();
```

**Problemas:** inconsistência na capitalização de variáveis, funções e classes, funções e chamadas de funções estão separadas, dificultando a leitura do fluxo, e a função processOrder deveria estar mais próxima de suas dependências.

---

**Exemplo correto segundo clean code:**
```javascript
const ITEMS_IN_CART = 3;
const ITEMS_IN_STOCK = 50;

const PRODUCTS = ['Laptop', 'Smartphone', 'Headphones'];
const CATEGORIES = ['Electronics', 'Accessories', 'Home Appliances'];

function placeOrder() {}
function cancelOrder() {}

class User {}
class Order {}

class OrderManager {
  constructor(order) {
    this.order = order;
  }

  processOrder() {
    this.getOrderDetails();
    this.sendInvoice();
    this.updateStock();
  }

  getOrderDetails() {
    const stock = this.checkStock();
    // ...
  }

  checkStock() {
    return db.lookup(this.order, 'stock');
  }

  sendInvoice() {
    // ...
  }

  updateStock() {
    const stock = this.checkStock();
    // ...
  }
}

const orderManager = new OrderManager(order);
orderManager.processOrder();
```

**Melhorias:** A capitalização está consistente, teve um uso adequado de maiúsculas e minúsculas nas variáveis, funções e classes, como ITEMS_IN_STOCK e placeOrder. A função processOrder está diretamente acima das funções auxiliares que ela utiliza, como getOrderDetails, sendInvoice, e updateStock, facilitando o fluxo de leitura. O código segue uma estrutura lógica de cima para baixo, refletindo um fluxo claro e fácil de entender.

---

<h2 id="descricao"> 7. Objetos e Estruturas de Dados </h2>

Objetos expõem as ações e ocultam os dados, o que facilita a adição de novos tipos de objetos sem precisar modificar as ações existentes, mas torna mais difícil a inclusão de novas atividades em objetos já existentes. Por outro lado, estruturas de dados expõem os dados e não possuem ações significativas, facilitando a adição de novas ações às estruturas de dados existentes, mas dificultando a inclusão de novas estruturas de dados em funções existentes.

Em um sistema, a escolha entre objetos e estruturas de dados depende da flexibilidade desejada. Quando se busca flexibilidade para adicionar novos tipos de dados, a opção por objetos é mais adequada. Quando a necessidade é adicionar novas ações, optar por tipos de dados e procedimentos faz mais sentido.

Utilizar getters e setters em objetos é uma prática recomendada porque oferece várias vantagens, como facilitar a modificação do comportamento dos acessos aos dados sem alterar os pontos de chamada no código, permite adicionar validações ao definir valores (set), por encapsular a representação interna dos dados promove maior flexibilidade, e torna mais fácil adicionar logs e tratamentos de erros.

**Exemplo ruim:**

```javascript
function createProduct() {
  return {
    stock: 0, // Propriedade pública
  };
}

const product = createProduct();
product.stock = 50; // Modificação direta
```

**Exemplo correto segundo clean code:**
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

Usar exceções é preferível a retornar códigos de erro ou null, pois facilita a identificação e o tratamento de problemas. Exceções tornam o código mais legível e robusto, separando a lógica principal do tratamento de erros. Evitar o uso de null como retorno ou argumento é crucial para prevenir erros inesperados, e o uso de objetos de caso especial pode eliminar a necessidade de verificações constantes de null.

Sempre trate erros capturados em try/catch com ações concretas, como logar adequadamente, notificar o usuário ou enviar relatórios para serviços de monitoramento. Não ignore promessas rejeitadas em código assíncrono.

**Exemplo ruim:**
```javascript
function processOrder(order) {
  const customer = getCustomer(order.id);
  if (customer !== null) {
    const paymentMethod = customer.getPaymentMethod();
    if (paymentMethod !== null) {
      if (!paymentMethod.isValid()) {
        console.log("Invalid payment method");
      } else {
        completeOrder(order);
      }
    } else {
      console.log("Payment method is null");
    }
  } else {
    console.log("Customer not found");
  }
}

getOrderData()
  .then((order) => {
    processOrder(order);
  })
  .catch((error) => {
    console.log("Error processing order:", error);
  });

try {
  updateInventory();
} catch (error) {
  console.log(error);
}
```
**Problemas:** faz uso de null como valor de retorno e muitas verificações de null,tratamento de erros com console.log, que não oferece um plano real de ação e  promessa rejeitada é tratada com console.log, o que pode ser facilmente ignorado.

---

**Exemplo correto segundo clean code:**
```javascript
function processOrder(order) {
  const customer = getCustomer(order.id) || new NullCustomer();
  const paymentMethod = customer.getPaymentMethod() || new NullPaymentMethod();

  if (!paymentMethod.isValid()) {
    throw new Error("Invalid payment method");
  }

  completeOrder(order);
}

getOrderData()
  .then((order) => {
    processOrder(order);
  })
  .catch((error) => {
    console.error("Error processing order:", error);
    notifyUserOfError(error);
    reportErrorToService(error);
  });

try {
  updateInventory();
} catch (error) {
  console.error("Inventory update failed:", error);
  reportErrorToService(error);
}
```

**Melhorias:** NullCustomer e NullPaymentMethod eliminam a necessidade de verificações de null. Em vez de console.log, o código usa console.error, notificação ao usuário e relatórios para um serviço, fornecendo um plano de ação claro. Promessas rejeitadas são tratadas com ações adequadas, como logar, notificar e reportar, em vez de simplesmente ignorar.

---

<h2 id="descricao"> 9. Limites </h2>

Ao integrar bibliotecas de terceiros, é importante entender seu funcionamento por meio de "testes de aprendizagem". Esses testes permitem explorar o comportamento da API sem comprometer a lógica principal da aplicação. Uma vez que a funcionalidade é compreendida, encapsule o uso da biblioteca em funções ou classes reutilizáveis para manter a configuração centralizada e clara.

**Exemplo ruim:**

```javascript
const winston = require('winston');

// Tentativa direta de uso da biblioteca sem testes ou estrutura clara
const logger = winston.createLogger({
    level: 'info',
    transports: [
        new winston.transports.Console()
    ]
});

logger.info('Logging direto sem testes.');

const anotherLogger = winston.createLogger({
    level: 'debug',
    transports: [
        new winston.transports.Console()
    ]
});

anotherLogger.debug('Outro logger sem configuração centralizada.');
```

**Problemas:** Uso direto da biblioteca sem testes para entender o comportamento, duplicação de código ao criar outro logger com configuração similar e configuração não centralizada, tornando o código mais difícil de manter e modificar.

---

**Exemplo correto segundo clean code:**

```javascript
const winston = require('winston');

// Teste de aprendizado para explorar a biblioteca de logging
function testLogCreate() {
    const logger = winston.createLogger({
        level: 'info',
        transports: [
            new winston.transports.Console()
        ]
    });
    logger.info('Testando logger básico');
}

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
    logger.info('Testando logger com formato personalizado');
}

// Centralizando a criação de loggers para uso em toda a aplicação
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
logger.info('Logger pronto para uso na aplicação.');
```

**Melhorias:** Foram criados testes para entender o comportamento do logger antes da implementação definitiva, a criação do logger foi centralizada em uma função, eliminando a duplicação e facilitando a manutenção e a função createLogger permite a reutilização da lógica de configuração em toda a aplicação.

---

<h2 id="descricao"> 10. Testes de Unidade </h2>

Testes de unidade são essenciais para garantir que o código de produção seja flexível e fácil de modificar. Testes claros e bem escritos permitem que os desenvolvedores façam mudanças com confiança, sabendo que erros serão detectados rapidamente. Para manter a qualidade, os testes devem ser rápidos, independentes, repetíveis, autovalidados e escritos no momento certo.

Além disso, cada teste deve se focar em um conceito por vez, evitando código duplicado ou complexidade desnecessária.

**Exemplo ruim:**

```javascript
import assert from 'assert';

describe('InventoryManager', () => {
  it('handles item stock and pricing', () => {
    let item = new InventoryManager('Laptop');
    item.addStock(50);
    assert.equal(item.getStock(), 50);

    item.setPrice(1200);
    assert.equal(item.getPrice(), 1200);

    item = new InventoryManager('Smartphone');
    item.addStock(30);
    assert.equal(item.getStock(), 30);

    item.setPrice(800);
    assert.equal(item.getPrice(), 800);
  });
});

import { get } from 'request';
import { writeFile } from 'fs';

get('https://api.shop.com/inventory', (requestErr, response) => {
  if (requestErr) {
    console.error(requestErr);
  } else {
    writeFile('inventory.json', response.body, (writeErr) => {
      if (writeErr) {
        console.error(writeErr);
      } else {
        console.log('File written');
      }
    });
  }
});
```
**Problemas:** os testes estão complexos por que possuem vários conceitos testados na mesma função, como estoque e preço. O código também está aninhado e difícil de manter com callbacks.

**Exemplo correto segundo clean code:**
```javascript
import assert from 'assert';

describe('InventoryManager', () => {
  it('handles item stock', () => {
    const item = new InventoryManager('Laptop');
    item.addStock(50);
    assert.equal(item.getStock(), 50);
  });

  it('handles item pricing', () => {
    const item = new InventoryManager('Laptop');
    item.setPrice(1200);
    assert.equal(item.getPrice(), 1200);
  });

  it('handles different items stock', () => {
    const item = new InventoryManager('Smartphone');
    item.addStock(30);
    assert.equal(item.getStock(), 30);
  });

  it('handles different items pricing', () => {
    const item = new InventoryManager('Smartphone');
    item.setPrice(800);
    assert.equal(item.getPrice(), 800);
  });
});

import { get } from 'request-promise';
import { writeFile } from 'fs-promise';

async function fetchInventory() {
  try {
    const response = await get('https://api.shop.com/inventory');
    await writeFile('inventory.json', response);
    console.log('File written');
  } catch (err) {
    console.error(err);
  }
}
```

**Melhorias:** os testes estão agora divididos por conceitos e foi simplificado com async/await, eliminando aninhamento de callbacks e melhorando a legibilidade.

---

<h2 id="descricao"> 11. Classes </h2>

Classes devem ser pequenas, focadas em uma única responsabilidade e coesas, seguindo o Princípio da Responsabilidade Única (SRP). Isso facilita a manutenção e evita a necessidade de modificações frequentes. Organize métodos relacionados próximos uns dos outros e prefira composição sobre herança, sempre que possível. Além disso, utilize padrões de design como injeção de dependência e o princípio do aberto/fechado para criar classes extensíveis sem a necessidade de alterar código existente.

**Exemplo ruim:**

```javascript
class Car {
  constructor(brand, model, year) {
    this.brand = brand;
    this.model = model;
    this.year = year;
    this.color = null;
  }

  setColor(color) {
    this.color = color;
  }

  saveCar() {
    console.log(`Saving ${this.brand} ${this.model}`);
  }

  updatePrice(price) {
    console.log(`Updated price to ${price}`);
  }

  calculateDepreciation() {
    const currentYear = new Date().getFullYear();
    const depreciation = (currentYear - this.year) * 0.1;
    console.log(`Depreciation: ${depreciation}`);
  }
}

const car = new Car('Tesla', 'Model S', 2020);
car.setColor('red');
car.saveCar();
car.updatePrice(70000);
car.calculateDepreciation();
```

**Problemas:** falta coesão por que a classe `car` está realizando múltiplas responsabilidades, como cálculo de depreciação e gerenciamento de preços. Há também duplicação no código por que métodos não relacionados estão centralizados em uma classe, dificultando a manutenção.

---

**Exemplo correto segundo clean code:**

```javascript
class Car {
  constructor(brand, model, year) {
    this.brand = brand;
    this.model = model;
    this.year = year;
    this.color = null;
  }

  setColor(color) {
    this.color = color;
    return this;  // Para encadeamento de métodos
  }

  save() {
    console.log(`Saving ${this.brand} ${this.model}`);
    return this;
  }
}

class CarPricing {
  constructor(car) {
    this.car = car;
  }

  updatePrice(price) {
    console.log(`Updated price for ${this.car.brand} ${this.car.model} to ${price}`);
  }
}

class DepreciationCalculator {
  constructor(car) {
    this.car = car;
  }

  calculate() {
    const currentYear = new Date().getFullYear();
    const depreciation = (currentYear - this.car.year) * 0.1;
    console.log(`Depreciation: ${depreciation}`);
  }
}

// Uso
const car = new Car('Tesla', 'Model S', 2020)
  .setColor('blue')
  .save();

const pricing = new CarPricing(car);
pricing.updatePrice(75000);

const depreciation = new DepreciationCalculator(car);
depreciation.calculate();
```

**Melhorias:** agora o código está visando a responsabilidade única, visto que foi feito a divisão da lógica entre classes Car, CarPricing e DepreciationCalculator, cada uma focada em uma responsabilidade única. O método setColor retorna this, permitindo encadeamento de métodos. Foi utilizado composição ao invés de herança, para separar funcionalidades como cálculo de depreciação e gestão de preços.

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