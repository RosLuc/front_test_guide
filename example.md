# Guia para desenvolvimento de testes Front-end web

## Sumário
1. [Introdução ao Guia](#1-introdução-ao-guia)
2. [Tipos de Testes](/types.md#2-tipos-de-testes)
   - [Testes Unitários](/types.md#21-testes-unitários)
   - [Testes de Integração](/types.md#22-testes-de-integração)
   - [Testes Funcionais](/types.md#23-testes-funcionais)
   - [Testes de Interface do Usuário](/types.md#24-testes-de-interface-do-usuário)
   - [Testes de Performance](/types.md#25-testes-de-performance)
   - [Testes de Segurança](/types.md#26-testes-de-segurança)
3. [Configuração do Ambiente de Testes](/config.md#3-configuração-do-ambiente-de-testes)
   - [Aplicação Alvo](/config.md#31-aplicação-alvo)
   - [Ferramentas para Teste](/config.md#32-ferramentas-para-teste)
   - [Configurar ambiente](/config.md#33-configurar-ambiente)
4. [Boas Práticas em Testes](/practices.md#4-boas-práticas-em-testes)
5. [Exemplos de Testes](/example.md#5-exemplos-de-testes)
   - [Testes Unitários](/example.md#51-testes-unitários)
   - [Testes de Integração](/example.md#52-testes-de-integração)
   - [Testes E2E](/example.md#53-testes-e2e)

## 5. Exemplos de Testes

Neste topico, será abordado testes na aplicação front-end.

### 5.1 Testes Unitários

Para iniciar os testes unitários, é necessário definir o que é uma unidade em seu projeto. Considerando que nossa aplicação alvo é um front-end em Next.js, podemos definir como unidades as funções utilitárias, que geralmente são utilizadas para manipular dados na aplicação, além dos hooks e contexts.

Em nossa aplicação alvo, o Me Contrata, temos as seguintes funções utilitárias no módulo de listagem de serviços.

```typescript
import { FilterType } from "@/types/filter-types";
import { PriorityTypes } from "@/types/priority-types";

export function getCategoryByType(type: FilterType) {

  switch (type) {
    case FilterType.PROGRAMMING:
      return 'PROGRAMMING';
    case FilterType.DESIGN:
      return 'DESIGN';
    default:
      return "";
  }
}

export function getFieldByPriority(priority: PriorityTypes) {

  switch (priority) {

    case PriorityTypes.NEWS:
      return { field: "created_at", order: "ASC" };
    case PriorityTypes.BIGGEST_PRICE:
      return { field: "price", order: "DESC" };
    case PriorityTypes.MINOR_PRICE:
      return { field: "price", order: "ASC" };
    default:
      return { field: "created_at", order: "ASC" };
  }
}

export function mountQuery(type: FilterType, priority: PriorityTypes) {

  const category = getCategoryByType(type);
  const field = getFieldByPriority(priority);

  return `?category=${category}&orderBy=${field.field}&order=${field.order}`;
};
```

Em geral, temos funções responsáveis pelo tratamento de Query Params de uma requisição, que envolvem várias condições e manipulação de strings. Por serem funções simples, sem a necessidade de renderizar conteúdos HTML da aplicação, o uso do Jest para implementar os testes é uma boa solução.

Para manter o projeto organizado, é recomendado criar um pasta 'specs' no diretório de utilitarios, e como foi configurado no jest, ele irá monitorar esses arquivos.

Para a função `getCategoryByType`, pode-se ver que temos uma condicional switch, o que implica ter casos de teste para cada `case` no código. Entretanto, no Jest podemos utilizar de funções especificas para não haver a necessidade de criar vários testes que fazem a mesma preparação para os casos de teste.

```typescript
describe('getCategoryByType', () => {

	it.each([
		{ title: 'ALL', input: FilterType.ALL, expected: '' },
		{ title: 'PROGRAMMING', input: FilterType.PROGRAMMING, expected: 'PROGRAMMING' },
		{ title: 'DESIGN', input: FilterType.DESIGN, expected: 'DESIGN' },
	])('returns the correct category for $title filter type', ({ input, expected }) => {

		const result = getCategoryByType(input);
		expect(result).toEqual(expected);
	});
});
```

Para começar os testes no Jest aplicamos o `describe`, no qual iremos definir a unidade a ser testada, no nosso caso, o `getCategoryByType`, uma das funções utilitarias da aplicação, a qual é responsavel por preparar uma parte da *query* para consultar os serviços ofertados pela plataforma.

Como pode ser visto na função, temos vários pontos com fluxos condicionais, e para cada um desses pontos será necessário um caso de teste para cobrir completamente a função. Porém, por se tratar de uma função simples, não será necessário definir várias implementações de casos de teste, pois o código seria semelhante, com diferenças apenas nas entradas e saídas dos testes. 

Dado isso, o Jest disponibiliza o método `each`, que, simplificadamente, pode ser visto como uma estrutura de laço, onde são definidos parâmetros que serão passados para a `callback` dos testes em cada iteração especificada. Tendo em vista nossa função `getCategoryByType`, precisariamos realizar três casos, dois para cada `case` do `switch` e um para o `default`.

Por se tratar de uma função simples, o teste pode ser escrito de forma concisa, utilizando o método `expect` em conjunto com `toEqual`. Dessa forma, definimos que "esperamos que o resultado da função seja igual a um valor esperado" para aquele caso de teste.

Para as demais funções desse mesmo arquivo, seguimos uma abordagem semelhante, sempre definindo testes simples, mas que possam cobrir de forma eficaz as funções utilitárias.

```typescript

describe('getFieldByPriority', () => {

	it.each([
		{ title: 'BIGGEST_PRICE', input: PriorityTypes.BIGGEST_PRICE, expected: { field: "price", order: "DESC" } },
		{ title: 'MINOR_PRICE', input: PriorityTypes.MINOR_PRICE, expected: { field: "price", order: "ASC" } },
		{ title: 'NEWS', input: PriorityTypes.NEWS, expected: { field: "created_at", order: "ASC" } },
		{ title: 'DEFAULT', input: 'DEFAULT', expected: { field: "created_at", order: "ASC" } },
	])('returns the correct category for $title filter type', ({ input, expected }) => {

		const result = getFieldByPriority(input as PriorityTypes);
		expect(result).toEqual(expected);
	});
});

describe('mountQuery', () => {

	it('returns the correct category for $title filter type', () => {

		const typeInput = FilterType.PROGRAMMING;
		const priorityInput = PriorityTypes.BIGGEST_PRICE;
		const result = mountQuery(typeInput, priorityInput);
		const expected = '?category=PROGRAMMING&orderBy=price&order=DESC';

		expect(result).toEqual(expected);
	});
});

```

### 5.2 Testes de Integração

Dado o seguinte componente do sistema, iremos construir seus teste utilizando a biblioteca do Jest.

```Typescript

import styles from "./styles.module.css";
import { formatPrice } from "@/utils/format-price";

interface ProductCardProps {
	image: string;
	title: string;
	price: number;
}

export function ProductCard(props: ProductCardProps) {  

	const price = formatPrice(props.price);

	return (
		<div className={styles.card}>
			<img src={props.image} />
			<div>
				<h3>{props.title}</h3>
				<div></div>
				<p>{price}</p>
			</div>
		</div>
	);
}

```

Esse teste foi desenvolvido para garantir que o componente `ProductCard` renderize corretamente os detalhes do produto. Por se tratar de um componente e ser mais complexo do que uma função utilitária, detalharemos os principais passos envolvidos na criação deste teste:

Primeiramente uremos usar as seguintes dependências para realizar os testes:

```Typescript

import { render, screen } from '@testing-library/react';
import { formatPrice } from '@/utils/format-price';
import { ProductCard } from '../index';

```

Aqui, você está importando funções e componentes necessários para o teste:

* `render` e `screen` do @testing-library/react são usados para renderizar o componente e acessar elementos no DOM renderizado.
* `formatPrice` é a função utilitária que formata o preço.
* `ProductCard` é o componente que você está testando.

Por termos uma dependência interna para o `formatPrice`, iremos definir um mock para que não afete nosso teste, utilizando o método `jest.mock` teremos acesso a essa definição.

```Typescript

jest.mock('../../../utils/format-price', () => ({
  formatPrice: jest.fn((price) => `$${price.toFixed(2)}`),
}));

```

Dado que estamos trabalhando com um componente HTML, precisamos renderizar seus elementos, para isso iremos usar o método `render` que irá "renderiazar" nosso componente, contruindo uma DOM virtual.

```Typescript

render(<ProductCard {...props} />);

```

**Dado que já temos uma "renderização" do componente, o que iremos validar com nossos testes?**

Iremos verificar se temos os elementos que foram construídos no componente de forma correta. Para isso, iremos buscar os elementos do componente por meio de seus textos esperados e tags HTML utilizadas.

```Typescript

const image = screen.getByRole('img');
const title = screen.getByText(props.title);
const price = screen.getByText(formatPrice(props.price));

```

Por fim, dado os elementos buscados é aplicar métodos do Jest para validar suas integridades.

```Typescript

expect(image).toHaveProperty('src', props.image);
expect(title).not.toBeNull();
expect(price).not.toBeNull();

```

Código completo do teste:

```Typescript

import { render, screen } from '@testing-library/react';
import { formatPrice } from '@/utils/format-price';
import { ProductCard } from '../index';

jest.mock('../../../utils/format-price', () => ({
    formatPrice: jest.fn((price) => `$${price.toFixed(2)}`),
}));

describe('ProductCardProps', () => {

    it('should render product details correctly', () => {

        const props = {
            image: 'https://example.com/image.jpg',
            title: 'Test Product',
            price: 19.99,
        };

        render(<ProductCard {...props} />);

        const image = screen.getByRole('img');
        const title = screen.getByText(props.title);
        const price = screen.getByText(formatPrice(props.price));

        expect(image).toHaveProperty('src', props.image);
        expect(title).not.toBeNull();
        expect(price).not.toBeNull();
    });
});

```

Como outro exemplo de teste, temos o de um componente que é utilizado com o componente testado anteriormente e conseguimos validar sua integração com o componente `ProductsList`, utilizando dos mesmos conceitos levantados anteriormente, mas sem aplicar um mock do componente filho.

```Typescript

import { render, screen } from '@testing-library/react';
import { ProductsList } from '../index';
import { useJobs } from '../../../hooks/useJob';

jest.mock('../../../hooks/useJob', () => ({
	useJobs: jest.fn()
}));

describe('ProductsList', () => {

	it('renders products and handles loading state', async () => {

		const mockData = [
			{ id: 1, name: 'Product 1', price: 100 },
			{ id: 2, name: 'Product 2', price: 200 },
		];

		(useJobs as jest.Mock).mockReturnValue({
			data: mockData,
			isPending: false,
		});

		render(<ProductsList />);

		expect(screen.getByText('Product 1')).not.toBeNull();
		expect(screen.getByText('Product 2')).not.toBeNull();
		expect(screen.getByText('R$ 1,00')).not.toBeNull();
		expect(screen.getByText('R$ 2,00')).not.toBeNull();
	});

	it('shows loading state while pending', () => {

		(useJobs as jest.Mock).mockReturnValue({
			data: [],
			isPending: true,
		});

		render(<ProductsList />);

		expect(screen.queryByText('Product 1')).toBeNull();
		expect(screen.queryByText('Product 2')).toBeNull();
	});
});

```

### 5.3 Testes E2E

1. Descrição do Teste (describe)

```Typescript
describe('ProductsList Component', () => {
  // Codigo do teste
});
```

`describe`: Bloco que agrupa um conjunto de testes relacionados. Aqui, estamos descrevendo o teste para o componente ProductsList.

2. Configuração Inicial (beforeEach)

```Typescript
beforeEach(() => {
  cy.intercept('GET', 'http://localhost:3001/job?category=&orderBy=created_at&order=ASC', {
    statusCode: 200,
    body: [
      { id: 1, name: 'Product 1', price: 100 },
      { id: 2, name: 'Product 2', price: 200 },
    ],
  }).as('getJobs');

  cy.visit('http://localhost:3000/jobs');
});
```

`cy.intercept`: Intercepta a solicitação de rede para GET http://localhost:3001/job e simula uma resposta com um status 200 e um corpo específico. Isso permite que você teste o componente com dados conhecidos, sem depender do servidor real.

`.as('getJobs')`: Dá um alias à interceptação para que possa ser referenciada mais tarde nos testes.

`cy.visit`: Navega para a URL onde o componente ProductsList está renderizado. Isso configura o ambiente de teste.

3. Teste 1: Verificar a Lista de Produtos

```Typescript
it('should display a list of products', () => {
  cy.wait('@getJobs');

  cy.get('[class*="list_container"]').should('exist');

  cy.get('[class*="card"]').should('have.length', 2);
  cy.contains('Product 1').should('be.visible');
  cy.contains('Product 2').should('be.visible');
});
```

`cy.wait('@getJobs')`: Aguarda a interceptação da solicitação @getJobs ser concluída para garantir que a resposta simulada foi recebida.

`cy.get('[class*="list_container"]')`: Seleciona o elemento que contém a classe que inclui list_container e verifica se ele existe na página.

`cy.get('[class*="card"]')`: Seleciona todos os elementos cuja classe inclui card e verifica se há exatamente 2 desses elementos.

`cy.contains('Product 1')` e `cy.contains('Product 2')`: Verifica se os textos 'Product 1' e 'Product 2' estão visíveis na página.

4. Teste 2: Verificar a Imagem de Placeholder

```Typescript
it('should show a placeholder image for products', () => {
  cy.wait('@getJobs');

  cy.get('[class*="card"] img')
    .should('have.attr', 'src')
    .and('include', 'https://via.placeholder.com/150');
});
```

`cy.wait('@getJobs')`: Aguarda novamente a interceptação da solicitação @getJobs ser concluída.

`cy.get('[class*="card"] img')`: Seleciona as imagens dentro dos elementos cuja classe inclui card.

`.should('have.attr', 'src')`: Verifica se a imagem tem o atributo src.

`.and('include', 'https://via.placeholder.com/150')`: Verifica se o valor do atributo src inclui a URL da imagem de placeholder fornecida.
