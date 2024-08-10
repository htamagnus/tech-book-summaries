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

1. **Funções Pequenas:** Funções devem ser pequenas, idealmente com poucas linhas. Funções menores são mais fáceis de entender e manter.

2. **Blocos e Indentação:** Blocos de código dentro de estruturas como if, else, e while devem conter apenas uma linha, preferencialmente uma chamada de função. Isso mantém a função pequena e permite usar nomes descritivos.

3. **Faça Apenas Uma Coisa:** Cada função deve fazer apenas uma coisa. Se você pode extrair outra função a partir do nome, a função original está fazendo mais de uma coisa.

4. **Um Nível de Abstração por Função:** Funções devem operar em um único nível de abstração. Misturar níveis de abstração dentro de uma função cria confusão e dificulta a leitura do código.

5. **Regra Decrescente:** O código deve ser lido de cima para baixo, como uma narrativa, onde cada função chama a próxima no nível de abstração seguinte, facilitando a compreensão.

6. **Instruções Switch:** Estruturas switch são difíceis de manter pequenas e focadas. Devem ser usadas com cautela, preferencialmente encapsuladas em classes de baixo nível e evitadas em favor do polimorfismo.

7. **Use Nomes Descritivos:** Funções devem ter nomes descritivos que expliquem exatamente o que fazem. Nomes longos e claros são preferíveis a curtos e enigmáticos. Bons nomes ajudam a entender o código sem a necessidade de comentários extensos.

8. **Parâmetros de Funções:** A quantidade ideal de parâmetros para uma função é zero. Funções com um ou dois parâmetros são aceitáveis, mas três ou mais devem ser evitados devido à complexidade de testes e entendimento.

9. **Formas Mônades Comuns:** Funções com um único parâmetro (mônades) geralmente fazem uma pergunta sobre o parâmetro (e.g., fileExists("MyFile")) ou o transformam em outra coisa (e.g., fileOpen("MyFile")). Nomes de funções devem deixar clara essa distinção. Evite funções com parâmetros de saída; prefira retornar o valor modificado.

10. **Parâmetros Lógicos:** Evite usar booleanos como parâmetros, pois isso indica que a função faz mais de uma coisa, o que pode ser confuso. Em vez disso, divida a função em duas, cada uma tratando um caso específico.

11. **Objetos como Parâmetros:** Quando uma função precisa de mais de dois ou três parâmetros, considere encapsulá-los em um objeto. Isso não apenas reduz a complexidade da função, mas também agrupa parâmetros relacionados em uma única entidade, tornando o código mais claro.

12. **Listas como Parâmetros:** Quando é necessário passar um número variável de parâmetros, use listas ou varargs. Isso ainda mantém as regras para mônades, díades e tríades aplicáveis, sem sobrecarregar a função com muitos parâmetros.

13. **Evite Efeitos Colaterais:** Funções devem fazer apenas o que o nome indica. Efeitos colaterais, como alterar o estado de variáveis externas ou iniciar sessões, criam dependências inesperadas e confusão. Funções devem ser focadas e livres de ações ocultas.

14. **Prefira Exceções a Códigos de Erro:** Usar exceções em vez de retornar códigos de erro mantém o código limpo e evita estruturas aninhadas complexas. O tratamento de erros fica separado do fluxo normal de execução, melhorando a clareza.

15. **Extraia Blocos Try/Catch:** Blocos try/catch podem confundir a lógica do código se misturados com o processamento normal. Extraia-os para funções separadas para isolar o tratamento de erros, tornando o código mais legível e fácil de manter.

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