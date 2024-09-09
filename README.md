# Guia para desenvolvimento de testes Front-end web

## Sumário
1. [Introdução ao Guia](#1-introdução-ao-guia)
2. [Tipos de Testes](#2-tipos-de-testes)
   - [Testes Unitários](#21-testes-unitários)
   - [Testes de Integração](#22-testes-de-integração)
   - [Testes Funcionais](#23-testes-funcionais)
   - [Testes de Interface do Usuário](#24-testes-de-interface-do-usuário-ui)
   - [Testes de Performance](#25-testes-de-performance)
   - [Testes de Segurança](#26-testes-de-segurança)

3. [Configuração do Ambiente de Testes](#3-configuração-do-ambiente-de-testes)
	- [Aplicação Alvo](#31-aplicação-alvo)
	- [Ferramentas para Teste](#32-ferramentas-para-teste)
	- [Configurar ambiente](#33-configurar-ambiente)

4. [Boas Práticas em Testes](#4-boas-práticas-em-testes)
5. [Exemplos de Testes](#5-exemplos-de-testes)
   - [Testes Unitários](#51-testes-unitários)
   - [Testes de Integração](#52-testes-de-integração)
   - [Testes Funcionais](#53-testes-funcionais)
6. [Depuração e Manutenção de Testes](#6-depuração-e-manutenção-de-testes)

## 1. Introdução ao Guia

Este guia tem como objetivo ajudar desenvolvedores front-end a realizar testes eficazes em suas aplicações web. Ele oferece uma introdução abrangente aos conceitos fundamentais de testes de software, proporcionando uma base sólida para a implementação de práticas de teste de qualidade.

Aqui, abordaremos desde os princípios básicos de testes até técnicas mais avançadas, cobrindo os diferentes tipos de testes que podem ser aplicados a projetos front-end. Além disso, discutiremos as melhores práticas para garantir que seus testes sejam eficazes, confiáveis e fáceis de manter.

Ao longo deste guia, você encontrará informações sobre:

- **Fundamentos dos Testes:** Compreenda a importância dos testes no ciclo de desenvolvimento e como eles contribuem para a qualidade e robustez do seu código.
- **Tipos de Testes:** Explore os diferentes tipos de testes, incluindo testes unitários, de integração, funcionais e de interface do usuário, e aprenda como e quando aplicar cada um.
- **Configuração do Ambiente de Testes:** Descubra como configurar seu ambiente de desenvolvimento para suportar testes automatizados e manuais.
- **Boas Práticas em Testes:** Conheça as melhores práticas para escrever, organizar e manter testes eficazes.
- **Exemplos Práticos:** Veja exemplos de testes para ilustrar como aplicar os conceitos discutidos em cenários reais.
- **Depuração e Manutenção:** Aprenda técnicas para depurar testes falhos e manter seus testes atualizados conforme seu projeto evolui.
- **Recursos Adicionais:** Encontre links para documentação, tutoriais e comunidades para expandir seu conhecimento e obter suporte adicional.

Este guia é projetado tanto para desenvolvedores iniciantes quanto para aqueles que desejam aprimorar suas habilidades em testes. Ao final, esperamos que você se sinta mais confiante na criação e execução de testes que garantam a qualidade e a robustez de suas aplicações front-end.


## 2. Tipos de Testes

Nesta seção, abordaremos os principais tipos de testes utilizados no desenvolvimento de front-end web, essenciais para garantir a qualidade e a confiabilidade da aplicação.

### 2.1 Testes Unitários
 
Testes unitários são projetados para verificar a funcionalidade de pequenas unidades de código, como funções ou métodos, de forma isolada. O objetivo é garantir que cada unidade opere conforme o esperado, sem dependências externas. Esses testes ajudam a identificar rapidamente problemas em partes específicas do código e facilitam a manutenção do software.

### 2.2 Testes de Integração
 
Testes de integração avaliam a interação entre diferentes módulos ou componentes da aplicação. Eles garantem que as partes do sistema funcionem bem juntas e que as interfaces entre esses módulos estejam corretas. Esses testes são essenciais para verificar se os dados fluem adequadamente entre componentes e se a aplicação como um todo se comporta de acordo com os requisitos.

### 2.3 Testes Funcionais
 
Testes funcionais focam em verificar se as funcionalidades da aplicação atendem aos requisitos especificados. Eles testam a aplicação do ponto de vista do usuário final, garantindo que os fluxos de trabalho e as funcionalidades sejam executados adequadamente. Esses testes são importantes para validar que a aplicação realiza as tarefas que os usuários esperam.

### 2.4 Testes de Interface do Usuário
 
Testes de User Interface (UI) verificam se os elementos visuais da aplicação são exibidos adequadamente e se as interações do usuário funcionam como esperado. Eles asseguram que a interface seja amigável e intuitiva, e que os elementos gráficos estejam corretos e bem posicionados. Esses testes ajudam a garantir uma boa experiência de usuário.

### 2.5 Testes de Performance
 
Testes de performance avaliam o desempenho da aplicação sob várias condições de carga. Eles medem aspectos como tempos de resposta, capacidade de processamento e uso de recursos para garantir que a aplicação funcione de maneira eficiente e escalável. Esses testes ajudam a identificar gargalos e a otimizar a performance da aplicação.

### 2.6 Testes de Segurança
 
Testes de segurança têm como objetivo identificar vulnerabilidades e fraquezas na aplicação que poderiam ser exploradas por atacantes. Eles verificam aspectos como autenticação, autorização e proteção contra ataques comuns (como XSS e SQL Injection). Garantir a segurança da aplicação é crucial para proteger dados sensíveis e garantir a integridade e a confidencialidade das informações.

## 3. Configuração do Ambiente de Testes

### 3.1 Aplicação Alvo

![Ambiente de Testes](img/mecontrata.png)

Para a elaboração dos testes, foi criada uma aplicação específica que servirá como ambiente de estudo. Esta aplicação foi projetada com o objetivo principal de demonstrar de maneira prática como os testes podem ser elaborados e aplicados no contexto do desenvolvimento front-end web. Ao proporcionar exemplos concretos de implementação de testes, pretende-se facilitar a compreensão dos leitores, permitindo-lhes visualizar diretamente como essas técnicas podem ser aplicadas em situações reais de desenvolvimento de software.

A aplicação em questão é desenvolvida utilizando o framework Next.js e se comunica com uma API REST. Para fins de demonstração e aprendizado, vamos utilizar o fluxo de listagem de busca como nosso laboratório de testes. Esse fluxo será o foco principal para apresentar exemplos práticos e boas práticas de testes em desenvolvimento web.

## 3.2 Ferramentas para Teste

A realização de testes eficazes em uma aplicação web é crucial para garantir que ela funcione adequadamente e ofereça uma experiência de usuário de alta qualidade. Para facilitar a criação e execução de testes, existem diversas ferramentas disponíveis que ajudam a automatizar e gerenciar esse processo. Neste guia, abordaremos duas das ferramentas mais populares no desenvolvimento front-end: Jest e Cypress.

### Jest

Jest é uma ferramenta de teste de JavaScript, amplamente utilizada para testar aplicações Node.js. É um framework de testes unitários e de integração que se destaca pela sua simplicidade e facilidade de configuração. Jest oferece uma série de funcionalidades, incluindo:

- **Testes Unitários e de Integração:** Permite escrever testes para verificar a funcionalidade de unidades de código e a interação entre diferentes partes da aplicação.
- **Mocks e Spies:** Facilita a criação de mocks e spies para simular e monitorar o comportamento de dependências e funções.
- **Cobertura de Código:** Fornece relatórios detalhados sobre a cobertura de código, ajudando a identificar áreas não testadas.
- **Execução Paralela de Testes:** Melhora a eficiência ao executar testes em paralelo, reduzindo o tempo total de execução.

**Exemplo de Uso:**  
Para testar uma função de utilitário que calcula descontos, você pode usar Jest para garantir que a função retorna os valores esperados para diferentes entradas.

```javascript
// Função gerar o preço real
function fitPrice(price) {
    return (preco / 100);
}

// Teste unitário com Jest
import { aplicarDesconto } from './utils';

test('should call fitPrice and return real price', () => {
    expect(fitPrice(100)).toBe(1);
});
```

### Cypress

Cypress é uma ferramenta de teste end-to-end projetada para a automação de testes de interface do usuário em aplicações web. É conhecida por sua simplicidade de configuração e pela integração poderosa com o navegador, o que permite realizar testes funcionais e de integração de forma eficaz. Algumas das características principais do Cypress incluem:

- **Testes End-to-End:** Permite simular interações reais do usuário e verificar o comportamento da aplicação em um navegador real, garantindo que a aplicação funcione conforme o esperado em situações de uso real.
- **Debugging Avançado:** Oferece uma interface de usuário interativa que facilita a depuração, permitindo visualizar o estado da aplicação em cada etapa do teste.
- **Snapshots e Vídeos:** Captura screenshots e grava vídeos dos testes em execução, o que ajuda na análise de falhas e na compreensão do comportamento da aplicação durante os testes.
- **Execução Rápida:** Executa testes de forma eficiente utilizando uma arquitetura que se comunica diretamente com o navegador, reduzindo o tempo total de execução dos testes.

**Exemplo de Uso:**  
Para testar uma página de login, você pode usar Cypress para simular o preenchimento do formulário e verificar se a mensagem de sucesso é exibida após a submissão.

```javascript
// Teste de login com Cypress
describe('Login Page', () => {
	it('should display success message when submitting the form', () => {
		// Acessar tela de Login
		cy.visit('/login');
		
		// Preencher campo de usuário
		cy.get('input[name="username"]').type('user');
		
		// Preencher campo de senha
		cy.get('input[name="password"]').type('password');
		
		// Acionar botão de login
		cy.get('button[type="submit"]').click();
		
		// Validar se o login foi efetuado com sucesso
		cy.contains('Login successful!').should('be.visible');
	});
});
```

### 3.3 Configurar ambiente

Neste tópico serão abordadas as configurações das ferramentas com foco no ambiente Linux; entretanto, os comandos também funcionam no CMD do Windows.

### Configuração do Jest

Sempre é recomendado seguir as orientações fornecidas na documentação oficial para garantir que sua configuração esteja correta e aproveitar ao máximo as funcionalidades da ferramenta. Para obter detalhes completos sobre a configuração e os recursos do Jest, consulte a [documentação oficial do Jest](https://jestjs.io/pt-BR/docs/getting-started).

#### Passos para Configuração

1. **Instale o Pacote Jest**

   Primeiro, adicione o Jest como uma dependência de desenvolvimento no seu projeto. Execute o seguinte comando no terminal:

   ```bash
   npm install --save-dev jest
   ```

2. **Gere o Arquivo de Configuração**

	Após instalar o Jest, você precisa gerar o arquivo de configuração. Execute o comando abaixo para inicializar a configuração padrão do Jest:

	```bash
	npx jest --init
	```

	Este comando criará um arquivo de configuração básico chamado `jest.config.js` (ou `jest.config.ts	`, se você estiver usando TypeScript). O arquivo de configuração permitirá que você personalize as opções de teste conforme necessário para seu projeto.

3. **Configure o Arquivo de Configuração**

	Após gerar o arquivo de configuração `jest.config.*`, você precisa ajustá-lo para garantir que os arquivos de teste sejam reconhecidos corretamente. 

	1. Abra o arquivo `jest.config.*` no seu editor de código.
	2. Localize a propriedade `testMatch` no arquivo de configuração.
	3. Atualize a configuração `testMatch` para incluir os seguintes padrões:

	```javascript
	testMatch: [
		"**/__tests__/**/*.[jt]s?(x)",
		"**/?(*.)+(spec|test).[tj]s?(x)"
	]
	```

	A configuração testMatch define quais arquivos devem ser considerados como arquivos de teste pelo Jest. Com essa configuração, o Jest buscará arquivos que correspondam aos padrões .spec.ts e .test.ts dentro dos diretórios __tests__ e em outros locais do projeto. Isso permite que você crie arquivos de teste com a extensão .spec.ts e o Jest os reconhecerá automaticamente durante a execução dos testes.

4. **Adicione um Script ao `package.json`**

	Para facilitar a execução dos testes, você pode adicionar um script ao seu arquivo `package.json`. Isso permite que você execute os testes com um comando simples. 

	1. Abra o arquivo `package.json` no seu projeto.
	2. Na seção `"scripts"`, adicione o seguinte script:

	```json
	{
		"scripts": {
			...
			"test": "jest",
			...
		}
	}
	```

### Cypress

Para garantir que você configure o Cypress corretamente e aproveite ao máximo suas funcionalidades, é altamente recomendável seguir as diretrizes e práticas recomendadas descritas na documentação oficial.

Para obter instruções detalhadas sobre como configurar o Cypress e entender seus recursos, consulte a [documentação oficial do Cypress](https://docs.cypress.io/guides/overview/why-cypress).

### Configuração do Cypress

1. **Instalação do Cypress**

   Para começar a usar o Cypress, você precisa instalá-lo como uma dependência de desenvolvimento em seu projeto. Abra seu terminal e execute o seguinte comando:

   ```bash
   npm install cypress --save-dev
   ```

2. **Inicialização do Cypress**

	Após a instalação, você pode inicializar o Cypress para configurar a estrutura de pastas padrão e adicionar arquivos de configuração. Execute o seguinte comando:

	```bash
	npx cypress open
	```

	Esse comando abrirá a interface gráfica do Cypress e criará automaticamente as pastas e arquivos necessários (cypress/ e cypress.json).

3. **Estrutura de Pastas**

	Após a inicialização, você verá uma estrutura de pastas semelhante a esta:

	```
	cypress/
	├── fixtures/
	├── integration/
	├── plugins/
	└── support/
	cypress.json
	```

	- `fixtures/`: Arquivos de dados para uso em testes.
	- `integration/`: Onde você escreve e armazena seus arquivos de teste.
	- `plugins/`: Scripts para customização do comportamento do Cypress.
	- `support/`: Arquivos e comandos auxiliares usados em seus testes.
	- `cypress.json`: Arquivo de configuração do Cypress.

4. **Configuração Básica**

	O arquivo cypress.json é usado para configurar as opções globais do Cypress. Você pode definir a URL base da sua aplicação para facilitar a escrita dos testes. Exemplo de configuração:

	```json
	{
		"baseUrl": "http://localhost:3000",
		"viewportWidth": 1280,
		"viewportHeight": 720
	}
	```

5. **Executando os Testes**

	Você pode executar os testes do Cypress usando a interface gráfica, que você abriu com o comando `npx cypress open`, ou executar os testes no terminal:

	```bash
	npx cypress run
	```
