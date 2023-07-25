# Informações sobre o padrão SOLID
Introdução com exemplos descrições aplicado ao java(type)script para representar cada letra do acrônimo, os exemplos mostram como geralmente se aplica sem o padrão, comparando com a aplicação do mesmo.
Aqui você pode ter uma noção básica sobre esses princípios.

## S - Princípio da Responsabilidade Única (Single Responsibility Principle - SRP)

O Princípio da Responsabilidade Única afirma que uma classe deve ter apenas uma única responsabilidade. Em outras palavras, cada classe deve ter apenas um motivo para mudar, o que ajuda a manter o código mais focado e compreensível.

### Exemplo em JavaScript

```javascript
// Exemplo sem seguir o SRP:
class Produto {
  constructor(nome, preco) {
    this.nome = nome;
    this.preco = preco;
  }

  calcularDesconto() {
    // Cálculo do desconto
  }

  salvarBancoDeDados() {
    // Lógica para salvar o produto no banco de dados
  }

  enviarNotificacao() {
    // Lógica para enviar notificação após salvar o produto
  }
}

// Exemplo seguindo o SRP:
class Produto {
  constructor(nome, preco) {
    this.nome = nome;
    this.preco = preco;
  }

  calcularDesconto() {
    // Cálculo do desconto
  }
}

class ProdutoDAO {
  salvarBancoDeDados() {
    // Lógica para salvar o produto no banco de dados
  }
}

class NotificacaoService {
  enviarNotificacao() {
    // Lógica para enviar notificação após salvar o produto
  }
}
```



## O - Princípio do Aberto/Fechado (Open/Closed Principle - OCP)

O Princípio do Aberto/Fechado estabelece que as classes devem estar abertas para extensão, mas fechadas para modificação. Isso significa que você pode estender o comportamento de uma classe sem precisar alterar seu código-fonte original.

### Exemplo em JavaScript

```javascript
// Exemplo sem seguir o OCP
class Forma {
  constructor() {}
  calcularArea() {}
}

class Retangulo extends Forma {
  constructor(largura, altura) {
    super();
    this.largura = largura;
    this.altura = altura;
  }

  calcularArea() {
    return this.largura * this.altura;
  }
}

class Circulo extends Forma {
  constructor(raio) {
    super();
    this.raio = raio;
  }

  calcularArea() {
    return Math.PI * this.raio * this.raio;
  }
}

// Adicionar um novo tipo de forma, por exemplo, um triângulo:
class Triangulo extends Forma {
  constructor(base, altura) {
    super();
    this.base = base;
    this.altura = altura;
  }

  calcularArea() {
    return (this.base * this.altura) / 2;
  }
}
```
O Princípio do Aberto/Fechado é importante para permitir que o código seja facilmente estendido para adicionar novos comportamentos ou funcionalidades sem precisar alterar o código já existente, evitando assim possíveis efeitos colaterais em outras partes do sistema.

## L - Princípio da Substituição de Liskov (Liskov Substitution Principle - LSP)

O Princípio da Substituição de Liskov enfatiza que as classes derivadas devem ser substituíveis por suas classes base sem afetar a integridade do programa. Em outras palavras, se uma classe A é um subtipo de uma classe B, então os objetos da classe B podem ser substituídos por objetos da classe A sem alterar o comportamento correto do programa.

### Exemplo em JavaScript

```javascript
class Retangulo {
  constructor(largura, altura) {
    this.largura = largura;
    this.altura = altura;
  }

  calcularArea() {
    return this.largura * this.altura;
  }
}

class Quadrado extends Retangulo {
  constructor(lado) {
    super(lado, lado);
  }
}

function imprimirArea(retangulo) {
  console.log(`Área: ${retangulo.calcularArea()}`);
}

const retangulo = new Retangulo(5, 10);
const quadrado = new Quadrado(5);

imprimirArea(retangulo); // Área: 50
imprimirArea(quadrado); // Área: 25
```

O Princípio da Substituição de Liskov é fundamental para garantir que as classes derivadas se comportem de maneira consistente com as classes base, permitindo assim o uso polimórfico das classes e simplificando o design do software.

## I - Princípio da Segregação de Interface (Interface Segregation Principle - ISP)

O Princípio da Segregação de Interface defende que uma classe não deve ser forçada a implementar interfaces que ela não utiliza. Em vez de criar interfaces abrangentes, é melhor criar interfaces específicas para cada contexto de uso. Dessa forma, as classes só implementarão as interfaces relevantes para suas funcionalidades.

### Exemplo em JavaScript

```javascript
// Exemplo sem seguir o ISP
class Animal {
  comer() {}
  voar() {}
  nadar() {}
}

class Pato extends Animal {
  voar() {
    // Implementação específica para patos voarem
  }

  nadar() {
    // Implementação específica para patos nadarem
  }
}

// Exemplo seguindo o ISP
class Animal {
  comer() {}
}

class Ave {
  voar() {}
}

class Nadador {
  nadar() {}
}

class Pato extends Animal, Ave, Nadador {
  // Implementações específicas para patos voarem e nadarem
}
```

O Princípio da Segregação de Interface é importante para evitar que as classes sejam sobrecarregadas com funcionalidades que não são relevantes para elas. Isso permite que o código seja mais modular e flexível, facilitando a manutenção e evolução do sistema.

# D - Princípio da Inversão de Dependência (Dependency Inversion Principle - DIP)

O Princípio da Inversão de Dependência afirma que as classes de alto nível não devem depender das classes de baixo nível. Em vez disso, ambas devem depender de abstrações. Isso pode ser alcançado através do uso de injeção de dependência, onde as dependências são injetadas nas classes em vez de serem criadas por elas.

## Exemplo em JavaScript

```javascript
// Exemplo sem seguir o DIP
class NotificacaoService {
  enviarNotificacao() {
    // Lógica para enviar notificação
  }
}

class PedidoService {
  constructor() {
    this.notificacaoService = new NotificacaoService();
  }

  criarPedido() {
    // Lógica para criar o pedido
    this.notificacaoService.enviarNotificacao();
  }
}

// Exemplo seguindo o DIP
class NotificacaoService {
  enviarNotificacao() {
    // Lógica para enviar notificação
  }
}

class PedidoService {
  constructor(notificacaoService) {
    this.notificacaoService = notificacaoService;
  }

  criarPedido() {
    // Lógica para criar o pedido
    this.notificacaoService.enviarNotificacao();
  }
}

// Uso das classes
const notificacaoService = new NotificacaoService();
const pedidoService = new PedidoService(notificacaoService);
```
O Princípio da Inversão de Dependência é fundamental para garantir que o código seja menos acoplado, mais flexível e mais fácil de ser testado. Ele permite que as dependências sejam substituídas de forma mais simples e promove um design de código mais modular e extensível.


# Aplicação do padrão em um projeto Angular
Vamos detalhar cada exemplo, implementando-os no Angular. Primeiramente, vamos criar um projeto Angular e, em seguida, implementar cada princípio SOLID em um componente específico.

## Diretórios

Passo 1: Criar um novo projeto Angular
Abra o terminal e execute o seguinte comando para criar um novo projeto Angular chamado "solid-example":

<b>Árvore de diretórios</b>

- src/
  - app/
    - produto-detalhe/
      - produto-detalhe.component.ts
      - produto-detalhe.component.html
      - produto-detalhe.component.css
      - produto-detalhe.component.spec.ts
    - carrinho/
      - carrinho.component.ts
      - carrinho.component.html
      - carrinho.component.css
      - carrinho.component.spec.ts
    - tabela/
      - tabela.component.ts
      - tabela.component.html
      - tabela.component.css
      - tabela.component.spec.ts
    - tabela-ordenavel/
      - tabela-ordenavel.component.ts
      - tabela-ordenavel.component.html
      - tabela-ordenavel.component.css
      - tabela-ordenavel.component.spec.ts
    - lista-itens/
      - lista-itens.component.ts
      - lista-itens.component.html
      - lista-itens.component.css
      - lista-itens.component.spec.ts
    - lista-produtos/
      - lista-produtos.component.ts
      - lista-produtos.component.html
      - lista-produtos.component.css
      - lista-produtos.component.spec.ts
    - lista-usuarios/
      - lista-usuarios.component.ts
      - lista-usuarios.component.html
      - lista-usuarios.component.css
      - lista-usuarios.component.spec.ts
    - upload-arquivos/
      - upload-arquivos.component.ts
      - upload-arquivos.component.html
      - upload-arquivos.component.css
      - upload-arquivos.component.spec.ts
    - exibir-lista-arquivos/
      - exibir-lista-arquivos.component.ts
      - exibir-lista-arquivos.component.html
      - exibir-lista-arquivos.component.css
      - exibir-lista-arquivos.component.spec.ts

## Snippet para geração

Criando Projeto

```
ng new solid-example
cd solid-example
```

Gerando componentes
```
ng generate component produto-detalhe
ng generate component carrinho
ng generate component tabela
ng generate component tabela-ordenavel
ng generate component lista-itens
ng generate component lista-produtos
ng generate component upload-arquivos
ng generate component lista-usuarios
ng generate component exibir-lista-arquivos
```
# Implementação

Agora, vamos implementar cada princípio SOLID em cada componente específico:

## Princípio da Responsabilidade Única (SRP):

Vamos aplicar o SRP no componente "ProdutoDetalheComponent". Esse componente será responsável apenas por exibir os detalhes de um produto.

<b>produto-detalhe.component.ts</b>

```javascript
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-produto-detalhe',
  template: `
    <div>
      <h2>Detalhes do Produto</h2>
      <p>Descrição: {{ descricao }}</p>
      <p>Preço: {{ preco }}</p>
    </div>
  `,
})
export class ProdutoDetalheComponent {
  @Input() descricao: string;
  @Input() preco: number;
}
```

## Princípio do Aberto/Fechado (OCP):
Vamos aplicar o OCP no componente "TabelaOrdenavelComponent". Esse componente extenderá o componente "TabelaComponent" e adicionará a funcionalidade de ordenação de dados.


<b>tabela.component.ts</b>


```javascript
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-tabela',
  template: `
    <table>
      <thead>
        <tr>
          <th *ngFor="let coluna of colunas">{{ coluna }}</th>
        </tr>
      </thead>
      <tbody>
        <tr *ngFor="let item of dados">
          <td *ngFor="let coluna of colunas">{{ item[coluna] }}</td>
        </tr>
      </tbody>
    </table>
  `,
})
export class TabelaComponent {
  @Input() colunas: string[];
  @Input() dados: any[];
}
```


<b>tabela-ordenavel.component.ts</b>

```javascript
import { Component, Input } from '@angular/core';
import { TabelaComponent } from './tabela.component';

@Component({
  selector: 'app-tabela-ordenavel',
  template: `
    <table>
      <thead>
        <tr>
          <th *ngFor="let coluna of colunas">{{ coluna }}</th>
        </tr>
      </thead>
      <tbody>
        <tr *ngFor="let item of dados | orderBy: colunaOrdenacao">
          <td *ngFor="let coluna of colunas">{{ item[coluna] }}</td>
        </tr>
      </tbody>
    </table>
  `,
})
export class TabelaOrdenavelComponent extends TabelaComponent {
  @Input() colunaOrdenacao: string;
}
```

## Princípio da Substituição de Liskov (LSP):
Vamos aplicar o LSP nos componentes "ListaProdutosComponent" e "ListaUsuariosComponent". Ambos estenderão o componente "ListaItensComponent", garantindo que podem ser substituídos por ele.

<b>lista-itens.component.ts:</b>

```javascript
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-lista-itens',
  template: `
    <ul>
      <li *ngFor="let item of itens">{{ item }}</li>
    </ul>
  `,
})
export class ListaItensComponent {
  @Input() itens: string[];
}
```

<b>lista-produtos.component.ts:</b>

```javascript
import { Component } from '@angular/core';
import { ListaItensComponent } from './lista-itens.component';

@Component({
  selector: 'app-lista-produtos',
  template: `
    <h2>Lista de Produtos</h2>
    <app-lista-itens [itens]="produtos"></app-lista-itens>
  `,
})
export class ListaProdutosComponent extends ListaItensComponent {
  produtos: string[] = ['Produto 1', 'Produto 2', 'Produto 3'];
}
```

<b>lista-usuarios.component.ts:</b>

```javascript
import { Component } from '@angular/core';
import { ListaItensComponent } from './lista-itens.component';

@Component({
  selector: 'app-lista-usuarios',
  template: `
    <h2>Lista de Usuários</h2>
    <app-lista-itens [itens]="usuarios"></app-lista-itens>
  `,
})
export class ListaUsuariosComponent extends ListaItensComponent {
  usuarios: string[] = ['Usuário 1', 'Usuário 2', 'Usuário 3'];
}
```

Princípio da Segregação de Interface (ISP):
Vamos aplicar o ISP nos componentes "UploadArquivosComponent" e "ExibirListaArquivosComponent". Cada componente implementará apenas a interface específica para sua funcionalidade.

<b>upload-arquivos.component.ts</b>

```javascript
import { Component } from '@angular/core';
import { UploadArquivos } from './interfaces/upload-arquivos.interface';

@Component({
  selector: 'app-upload-arquivos',
  template: `
    <input type="file" (change)="onFileChange($event)" />
  `,
})
export class UploadArquivosComponent implements UploadArquivos {
  onFileChange(event: any): void {
    // Lógica para fazer o upload do arquivo
  }
}
```
<b>exibir-lista-arquivos.component.ts:</b>

```javascript
import { Component } from '@angular/core';
import { ExibirListaArquivos } from './interfaces/exibir-lista-arquivos.interface';

@Component({
  selector: 'app-exibir-lista-arquivos',
  template: `
    <h2>Lista de Arquivos</h2>
    <ul>
      <li *ngFor="let arquivo of arquivos">{{ arquivo }}</li>
    </ul>
  `,
})
export class ExibirListaArquivosComponent implements ExibirListaArquivos {
  arquivos: string[] = ['arquivo1.txt', 'arquivo2.png', 'arquivo3.doc'];
}
```

## Princípio da Inversão de Dependência (DIP):
Vamos aplicar o DIP no componente "CarrinhoComponent". Em vez de criar uma instância diretamente, vamos injetar o serviço de gerenciamento do carrinho.

<b>carrinho.component.ts:</b>

```javascript
import { Component } from '@angular/core';
import { CarrinhoService } from './carrinho.service';

@Component({
  selector: 'app-carrinho',
  template: `
    <div>
      <h2>Carrinho de Compras</h2>
      <ul>
        <li *ngFor="let item of carrinhoService.itens">{{ item }}</li>
      </ul>
    </div>
  `,
})
export class CarrinhoComponent {
  constructor(private carrinhoService: CarrinhoService) {}
}
```
<b>Interfaces usadas

```javascript
// arquivo: interfaces/upload-arquivos.interface.ts
export interface UploadArquivos {
  onFileChange(event: any): void;
}

// arquivo: interfaces/exibir-lista-arquivos.interface.ts
export interface ExibirListaArquivos {
  arquivos: string[];
}
```
Essas interfaces são usadas nos exemplos dos princípios SOLID apresentados anteriormente para ilustrar a aplicação dos princípios em componentes Angular. Elas definem os contratos que os componentes devem seguir para garantir a conformidade com os princípios SOLID.



# Conclusão

Neste exemplo, estamos aplicando os princípios SOLID em componentes Angular para tornar o código mais organizado, flexível e fácil de manter. Ao seguir esses princípios, você pode desenvolver aplicativos mais robustos e escaláveis, facilitando o trabalho da equipe de desenvolvimento no longo prazo.
