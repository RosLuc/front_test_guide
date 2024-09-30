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

## 4. Boas Práticas em Testes

1. **Escreva testes pequenos e focados**
Os testes devem abranger pequenas unidades de código, como funções e componentes, de forma isolada. Isso facilita a identificação de falhas, tornando a depuração mais eficiente e simplificando a manutenção dos testes. A independência dos testes também ajuda a detectar problemas rapidamente em futuras atualizações ou refatorações.

2. **Siga a pirâmide de testes**
Utilize a pirâmide de testes como referência, priorizando os testes unitários, seguidos pelos testes de integração e, por último, os testes end-to-end. Essa estratégia assegura uma cobertura eficiente com menor custo de manutenção.

![Pirâmide](img/pi.png)

3. **Evite dependências externas**
Sempre evitar trabalhar com dependências externas em seus testes, utlize de *mocks* para simular estas dependências e trate sempre como seu funcionamento esperado. 

4. **Teste o que importa**
Teste o comportamento do sistema, e não as implementações internas. Se um componente ou função for refatorado sem mudar sua funcionalidade, os testes não devem falhar. Isso garante que os testes validem o resultado final, não os detalhes de como ele é alcançado.

5. **Escreva testes legíveis**
Os testes devem ser fáceis de entender por outras pessoas, assim como o código principal deve seguir as práticas de *clean code*. Testes também são código e, portanto, precisam aderir a boas práticas de legibilidade e organização. É importante lembrar que a manutenção de um sistema inclui tanto o código da aplicação quanto seus testes, garantindo que ambos sejam claros e fáceis de manter ao longo do tempo.

6. **Garanta cobertura de código adequada**
Embora a cobertura de 100% não seja sempre o objetivo, é importante garantir que os cenários críticos e as funcionalidades principais sejam testados.

7. **Mantenha os testes atualizados**
Sempre que o código for atualizado, os testes também devem ser revisados. Manter testes obsoletos ou irrelevantes pode comprometer a qualidade geral do sistema. Certifique-se de que os testes acompanhem as mudanças no código, garantindo sua relevância e eficácia na detecção de possíveis falhas.
