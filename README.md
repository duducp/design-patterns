# Design Pattern
Resumão dos Design Patterns do GOF

**Índice**   
1. [Singleton](#cs1)
2. [Prototype](#cs2)
3. [Builder](#cs3)
4. [Factory Method](#cs4)
5. [Abstract Factory](#cs5)

## Criação
Foco na criação de objetos.

### Singleton <a name="cs1"></a>
O **Singleton** tem o objetivo de garantir que a classe tenha no máximo uma única instância durante todo o ciclo de vida do aplicativo. Utilizar o Singleton, evita a criação excessiva de elementos estáticos em uma aplicação.

![Singleton](https://lh3.googleusercontent.com/NBRL42gZakADUrGdzNKtZofk9jXbXZo_ZSv5EwAdP_fOJU8Aq-ZQ0-JJmBKqO0L0klvvtqvKtlA)

    public class Singleton {

      private static Singleton instancia;
    
      private Singleton() {
      }
    
      public static synchronized Singleton obterInstancia() {
        if (instancia == null) {
          instancia = new Singleton();
        }
        return instancia;
      }
    
    }
Elementos principais:
- É uma classe;
- Tem no máximo uma única instância durante todo o ciclo de vida do aplicativo;
- Seu atributo privado de nome instancia, do tipo Singleton, armazena a única instância depois de criada, da classe Singleton;
- O construtor dessa classe é privado, protegido de acesso externo;

Tira dúvidas:
- Por que o construtor deve ser privado?

Por um simples motivo: não permitir instanciar a classe “do seu lado de fora”.
- Como ela é instanciada?

A resposta está no método obterInstancia(). Esse método é responsável por criar e retornar a instância única de Singleton. Ele verifica se a classe já possui uma instância ativa (no atributo instancia). Se ela já tem uma instância ativa, o método apenas a retorna; se ainda não tem uma instância ativa, o método cria uma instância, atribui ela ao atributo instancia e a retorna. É interessante que o método obterInstancia() seja seguro em relação a threads (thread-safe), pois caso contrário podem ocorrer anomalias. O principal problema que pode ocorrer é uma thread sacana sobrescrever a instância criada por outra thread.

Referências:
[Matera](http://www.matera.com/blog/post/design-patterns-singleton)

### Prototype<a name="cs2"></a>
O **Prototype** é um padrão que especifica os tipos de objetos a serem criados utilizando um protótipo. Ele fornece um método alternativo para instanciar novos objetos através da cópia ou clone de uma instância existente. A criação de uma nova instância é bastante custosa, assim esse padrão ajuda a resolver esse problema.

Um exemplo clássico do padrão Prototype é quando se tem um documento padrão: quando for preciso utilizá-lo novamente, ao invés de criá-lo novamente, basta realizar uma cópia dele com as alterações necessárias.

Esse padrão é muito utilizado quando o sistema não precisa se preocupar com o mecanismo de criação dos produtos e quando é preciso instanciar classes em tempo de execução. O problema do Prototype é que sempre será necessário implementar o mecanismo de clone em cada subclasse.

![Phototype](https://lh3.googleusercontent.com/Hr-KuWv99dD6_Yi26qLO74FuhYl_a_5WBqdt_UApZpczb515d38FIafSLUiMouQT_NS45wEZdeHh)

Referências:
[DevMedia](https://www.devmedia.com.br/implementando-padroes-criacionais-em-java/34185)

### Builder<a name="cs3"></a>
O padrão **Builder** é um padrão de projetos de software comum que é usado para encapsular a lógica de construção de um objeto. Este padrão é frequentemente utilizado quando o processo de construção de um objeto é considerado complexo e também é adequado quando se trata da construção de representações múltiplas de uma mesma classe.

**Componentes:**

O padrão em questão é composto por quatro componentes básicos que são a Interface (ou classe abstrata) Builder, o concrete builder (construtor concreto), o Director (Diretor) e o product (produto).

**Como tudo funciona:**

Primeiramente, o client (cliente) poderá ser de certa forma, ou um objeto a parte ou mesmo o cliente real que chamará o método main() da aplicação, iniciando assim as classes Builder e Director.

A classe Builder representa o nosso objeto complexo que precisa ser construído em termos de objetos e tipos mais simples.

O construtor da classe Director recebe um objeto Builder como sendo um parâmetro através do cliente e é responsável por chamar os métodos apropriados da classe Builder.

A fim de fornecer a classe cliente com uma interface para todos os construtores concretos, a classe Builder deve ser uma classe abstrata. Desta forma, podemos adicionar novos tipos de objetos apenas definindo a estrutura e reutilizando a lógica para o processo real da construção. O cliente é o único que precisa saber sobre os novos tipos, já a classe Director, precisa saber apenas quais os métodos que precisará chamar.

![Builder](https://lh3.googleusercontent.com/7j82LV75khrQovj7_4MVwHuea-KKtMUoCdHAGbmngNDN51bM8L5YTY9PG4SGmHpOUUkLozTu-pk)

Referências:
[DevMedia](https://www.devmedia.com.br/design-patterns-aplicando-os-padroes-builder-singleton-e-prototype/31023)

### Factory Method<a name="cs4"></a>
O **Factory Method** é um padrão que define uma interface para criação de um objeto, mas permite que as subclasses decidam qual classe instanciar.

Um exemplo de utilização do Factory Method são as aplicações Windows, que possuem diferentes banco de dados como Oracle e SQL Server. Assim, sempre que for preciso inserir informações no banco de dados é preciso criar uma SqlConnection ou uma OracleConnection. Se isso for feito em um if-else teremos muito código e uma manutenção complicada.

Para resolver este problema basta utilizar o Factory Method, que possui uma estrutura básica com uma classe abstrata. As subclasses serão derivadas dessa classe e terão a responsabilidade do processo de instanciação.

Este padrão é útil quando a responsabilidade da criação de objetos deve ser das subclasses e quando queremos que o sistema fique com menos acoplamento possível.

![enter image description here](https://lh3.googleusercontent.com/8iMdxKCHwTdRxxL6XyjDtDNX8rKC3pMU6c_Tv9cfY_E-xstGOZxS7TMpqrxxnch_l30kVe6oUq6o)

Referências:
[DevMedia](https://www.devmedia.com.br/implementando-padroes-criacionais-em-java/34185)

### Abstract Factory<a name="cs5"></a>
O **Abstract Factory** é um padrão permite a criação de famílias de objetos relacionados ou dependentes por meio de uma única interface e sem que a classe concreta seja especificada. Resumidamente o seu objetivo principal é remover código de criação (aquele com a palavra reservada **new**) de nossas classes de negócio. 

Você irá perceber que ele é muito similar ao Factory Method, alias ele tem na composição dele a implementação de vários Factory Method, isso porque o Abstract Factory trabalha com a criação de famílias de objetos.

![Abstract Factory](https://lh3.googleusercontent.com/ZIkXsrq7F2BwnnWwZGCWDB6nVzDW6PssxUZUH8Lc8JZ_TQJC5j3DOVVIDExapJr7uYwu65sreTvi)

No diagrama é possível ver a real diferença entre o Abstract Factory e o Factory Method. Uma família de métodos de criação em Abstract Factory. Outra diferença que é notável é que enquanto Factory Method é comumente utilizado como herança o Abstract Factory é comum como composição.

**Ponto Negativo:**
-   Implementar um Abstract Factory quando um simples Simple Factory ou Factory Method seriam o suficiente, pode piorar a performance do projeto, ainda mais na leitura dele.

**Ponto Positivo:**
-   Como com todos os outros padrões de projeto, utilizar o Abstract Factory implica também em adicionar, ao menos em parte do projeto, uma linguagem universal aos programadores. Padrões tendem a serem conhecidos por muitos developers e na leitura do código a identificação de uso de um padrão já alivia na necessidade de ter de destrinchar o código para entendê-lo;
-   Encapsulamento do código de criação em pontos únicos do projeto removendo também com isso o forte acoplamento entre classes que não deveriam ter um alto nível de relacionamento umas com as outras;

Referências:
[Thiengo](https://www.thiengo.com.br/padrao-de-projeto-abstract-factory)
[Brizeno](https://brizeno.wordpress.com/category/padroes-de-projeto/abstract-factory/)

#### Utilitários:
Exemplo de Padrões de Projetos: [MarcosX](https://github.com/MarcosX/Padr-es-de-Projeto)

Os arquivos estão como um projeto do eclipse, então basta colocar no seu Workspace e fazer o import.
