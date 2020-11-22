# Princípios SOLID

##### Autor: Martin Heckmann

Apresentados por [Robert C. Martin](https://en.wikipedia.org/wiki/Robert_C._Martin) em 2000, os princípios de design **SOLID** para programação orientada a objetos tem o objetivo de tornar o design de software mais compreensíveis, flexíveis e com uma manutenção mais simples. Neste trabalho apresentaremos o primeiro destes princípios, o SRP-Single Responsability Principle (Princípio da Responsabilidade Única).

## Single Responsability Principle
O princípio de responsabilidade única diz que: 
> Cada classe deve ter um, e somente um, motivo para mudar.
Ou seja, cada classe deve ter uma unica responsabilidade ou tarefa dentro do programa. **Faça uma unica coisa mas faça bem feito.**

Robert Martin também diz que esse princípio é sobre pessoas. Assim, ao se utilizar corretamente o princípio da responsabilidade única, não devem ocorrer sobreposições nas obrigações das pessoas ou equipes trabalhando no programa.

Quando não utilizamos o princípio da responsabilidade única, temos o que é conhecido como **GOD CLASS**, uma classe que faz de tudo.

Isso pode acabar gerando alguns problemas como: 
- Falta de coesão: a classe assume responsabilidades que não deveriam ser dela;
- Dificuldades no reaproveitamento do código;
- Dificuldade na implementação de testes automatizados;
- Icompatibilidade de módulos: Com varias pessoas alterando o mesmo módulo por motivos diferentes, as incompatibilidades são mais frequentes;
- Dificuldade no versionamento;
- Conflitos de merge;

Ilustraremos melhor esse conceito com um exemplo. Tomemos como exemplo a classe a seguir utilizada para análise de reviews de produtos.
```class Review_Analysis:
         def __init__(self,data):
              self.data = data
         
         
         def pre_process(self):
                  //realiza o pré-processamento dos dados
         
         
         def sentiment_analysis(self):
                  //código que faz a análise de sentimentos das reviews
                  
         
         def visualization(self):
                  //código que mostra os resultados obtidos
                  
                  
         def save_to_file(self, filename):
                 //Cria um arquivo e salva os dados
  ```             
Nossa classe então, além de ter os dados principais, contém 4 métodos:
- pre_process
- sentiment_analysis
- visualization
- save_to_file
Essa classe viola o princípio da responsabilidade única visto que, caso seja necessário mudar a forma como fazemos a visualização, teriamos que mudar a classe. Nossa classe deve ter somente um motivo para mudar, e nesse caso o motivo deve ser a análise de sentimentos.

Pior ainda, os métodos presentes provavelmente seriam de responsabilidade de grupos diferentes; o pré-processamento poderia ser de responsabilidade de uma equipe de engenharia de dados, a análise de sentimentos por uma equipe de ciência de dados, a visualização por uma equipe de front end e a lógica de persistência, que nesse caso é somente salvar para um arquivo mas poderia ser salvar num banco de dados, poderia ser responsabilidade de uma equipe de infra.

Podemos resolver isso separando a classe em classes mais coesas. Criamos então outras 3 classes que lidam exclusivamente com a visualização, o pré-processamento e com a lógica de persistência. Preferencialmente, essas classes novas devem também estar em outro arquivo, assim, caso a pessoa ou grupo de pessoas responsavel por pela parte de código que deve ser mudada não correm o risco de alterar alguma outra parte do programa.

```class Pre_Process:
          def __init__(self,data):
                  self.data = data
          
          def process(self):
                  //realiza o pré processamento dos dados
```
```class Visualization:
          def __init__(self, data):
                  self.data = data
          
          def show(self):
                  //mostra a visualização dos dados
 ```
 ```class SaveToFile:
          def __init__(self, data):
                  self.data = data
                  
          def save(self, filename):
                  //Cria um arquivo e salva os dados
```
Deixando assim a classe review_analysis somente com a tarefa de fazer a analise de sentimentos dos dados e, assim, cada classe tem somente uma responsabilidade no programa.


### Links
Alguns links que ajudaram na pesquisa deste trabalho e que ficam como recomendação para conhecer melhor sobre o princípio de responsabilidade única e outros dos princípios **SOLID.**

- <https://www.freecodecamp.org/news/solid-principles-explained-in-plain-english/>
- <https://medium.com/desenvolvendo-com-paixao/o-que-%C3%A9-solid-o-guia-completo-para-voc%C3%AA-entender-os-5-princ%C3%ADpios-da-poo-2b937b3fc530>
- <https://www.youtube.com/watch?v=L2m-S0Pj_Xk>
- <https://www.digitalocean.com/community/conceptual_articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design#single-responsibility-principle>
