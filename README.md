# 💼 CatchaTechJob

O **CatchaTechJob** é uma aplicação web desenvolvida para simular uma plataforma de análise de compatibilidade entre candidatos e vagas da área de tecnologia.

O candidato informa seus dados, área de atuação, habilidades e tempo de experiência. A aplicação utiliza essas informações para comparar o perfil informado com os requisitos das vagas disponíveis.

Como resultado, o sistema apresenta:

- percentual de compatibilidade;
- classificação da compatibilidade;
- habilidades encontradas;
- habilidades que ainda precisam ser desenvolvidas;
- requisito mínimo de experiência;
- indicação se o candidato atende à experiência exigida;
- melhor vaga ou melhores vagas encontradas;
- recomendação de tecnologias para estudo.

O projeto foi desenvolvido utilizando **HTML, CSS e JavaScript puro**, sem frameworks, back-end ou banco de dados.

---

## 🎯 Objetivo do projeto

O objetivo do CatchaTechJob é aplicar de forma integrada os conteúdos estudados durante o primeiro módulo da formação Front-End.

O projeto trabalha conceitos como:

- HTML semântico;
- CSS;
- Flexbox;
- responsividade Mobile First;
- JavaScript;
- manipulação do DOM;
- eventos;
- formulários;
- validação;
- arrays;
- métodos de array;
- objetos;
- Programação Orientada a Objetos;
- classes;
- herança;
- callbacks;
- closures;
- Promises;
- `async/await`;
- Fetch API;
- LocalStorage;
- ES Modules;
- acessibilidade;
- SEO;
- Geolocation API;
- consumo de API externa.

---

# 👤 Como utilizar a aplicação

Ao abrir o CatchaTechJob, o usuário encontra a tela principal da aplicação.

Para realizar uma análise de perfil:

1. Clique no botão **Sou candidato**.
2. O formulário de candidato será exibido.
3. Preencha seu nome.
4. Informe sua idade.
5. Escolha sua principal área de atuação:
   - Front-end;
   - Back-end;
   - Full Stack.
6. Selecione as tecnologias ou ferramentas que você conhece.
7. Informe seu tempo de experiência.
8. Clique no botão **Encontrar vagas**.
9. A aplicação exibirá a mensagem **Carregando vagas...**.
10. As vagas serão carregadas a partir do arquivo `vagas.json`.
11. O sistema analisará o perfil informado.
12. Os cards das vagas serão exibidos mostrando a compatibilidade entre o candidato e cada oportunidade.

O perfil informado também é salvo no navegador através do `localStorage`.

Por isso, ao atualizar ou abrir novamente a aplicação, o perfil pode ser recuperado automaticamente.

Para remover o perfil salvo e realizar uma nova análise, basta utilizar **Começar novamente**.

---

# ⚙️ Fluxo da aplicação

```text
Usuário acessa a aplicação
        ↓
Clica em "Sou candidato"
        ↓
Preenche o formulário
        ↓
Validação dos dados
        ↓
Perfil salvo no LocalStorage
        ↓
Carregamento das vagas com fetch
        ↓
Transformação do JSON em objetos Vaga
        ↓
Filtro por categoria
        ↓
Análise de compatibilidade
        ↓
Ordenação dos resultados
        ↓
Identificação da melhor vaga
        ↓
Recomendação de estudos
        ↓
Renderização dos cards na tela
```

---

# 🧮 Cálculo de compatibilidade

A compatibilidade é calculada comparando as habilidades do candidato com os requisitos de cada vaga.

A lógica utilizada é:

```text
percentual =
(habilidades encontradas / total de requisitos) × 100
```

### Exemplo

Uma vaga possui os seguintes requisitos:

```text
HTML
CSS
JavaScript
Git
Responsividade
```

O candidato possui:

```text
HTML
CSS
JavaScript
Git
```

Nesse caso foram encontradas 4 habilidades de um total de 5 requisitos.

```text
4 / 5 = 0,8

0,8 × 100 = 80%
```

Portanto:

```text
Compatibilidade: 80%
```

No JavaScript o resultado final é arredondado utilizando:

```javascript
Math.round(percentual)
```

---

# 📊 Classificação da compatibilidade

Após calcular o percentual, a aplicação classifica cada vaga em três níveis.

```text
80% até 100% → Alta
50% até 79% → Média
0% até 49% → Baixa
```

Essa lógica está implementada no método:

```javascript
classificar(percentual)
```

da classe `Vaga`.

Exemplo:

```text
90% → Alta
65% → Média
30% → Baixa
```

A classificação facilita a visualização do nível de compatibilidade entre candidato e vaga.

---

# ✅ Habilidades encontradas

Para cada vaga, o sistema verifica quais requisitos também aparecem na lista de habilidades do candidato.

Essas tecnologias são apresentadas no card como **Habilidades encontradas**.

A comparação utiliza o método:

```javascript
filter()
```

---

# 📚 Habilidades a desenvolver

Os requisitos da vaga que não foram encontrados no perfil do candidato são separados em outra lista.

Eles aparecem no card como **Habilidades a desenvolver**.

Essas informações também são utilizadas posteriormente para gerar a recomendação de estudos.

---

# ⭐ Melhor vaga

Depois que todas as vagas são analisadas, o sistema procura o maior percentual de compatibilidade encontrado.

Para isso é utilizado:

```javascript
reduce()
```

Exemplo:

```text
Vaga A → 60%
Vaga B → 80%
Vaga C → 100%
Vaga D → 40%
```

Nesse caso:

```text
Maior compatibilidade = 100%
```

A vaga C será apresentada na área **Melhor vaga para o seu perfil**.

---

# 🤝 Tratamento de empate

O CatchaTechJob também trata situações em que duas ou mais vagas possuem o mesmo maior percentual.

Exemplo:

```text
Vaga A → 100%
Vaga B → 100%
Vaga C → 80%
```

Nesse caso, o sistema não utiliza um critério secundário para escolher apenas uma vaga.

As duas vagas com 100% são consideradas as melhores opções.

A interface passa a mostrar **Melhores vagas para o seu perfil** e apresenta todas as vagas empatadas.

Para localizar essas vagas é utilizado:

```javascript
filter()
```

comparando cada resultado com o maior percentual encontrado.

Portanto, atualmente o projeto possui **tratamento de empate**, e não um desempate por salário, experiência ou outro critério.

Um critério adicional de desempate pode ser implementado futuramente.

---

# 💼 Experiência profissional

Além das habilidades técnicas, cada vaga possui um valor mínimo de experiência.

O sistema compara:

```javascript
experienciaCandidato >= experienciaMinima
```

Caso a condição seja verdadeira, o card apresenta **Atende ao requisito**.

Caso contrário, apresenta **Ainda não atende ao requisito**.

A experiência é analisada separadamente do cálculo das habilidades.

Por isso, ela não altera diretamente o percentual de compatibilidade.

---

# 📚 Recomendação de estudos

Depois de analisar as vagas, o sistema reúne as habilidades que estão faltando no perfil do candidato.

Essas habilidades são contadas para identificar quais aparecem com maior frequência.

Exemplo:

```text
React → falta em 3 vagas
Docker → falta em 2 vagas
SQL → falta em 3 vagas
AWS → falta em 1 vaga
```

Nesse caso, a recomendação será:

```text
React
SQL
```

porque são as tecnologias ausentes que aparecem com maior frequência.

---

# 🧬 Programação Orientada a Objetos

O motor de compatibilidade utiliza Programação Orientada a Objetos.

A classe principal é:

```javascript
class Vaga
```

Ela possui construtor, atributos, métodos e uso de `this`.

Entre os métodos estão:

```javascript
calcularCompatibilidade()
classificar()
verificarExperiencia()
getArea()
analisar()
```

---

# 🧬 Herança e método `getArea()`

Além da classe principal `Vaga`, o projeto possui três subclasses:

```javascript
class VagaFrontEnd extends Vaga
class VagaBackEnd extends Vaga
class VagaFullStack extends Vaga
```

A classe `Vaga` possui o método:

```javascript
getArea() {
  return "Desenvolvimento";
}
```

Esse método é sobrescrito pelas subclasses.

Exemplo:

```javascript
class VagaFrontEnd extends Vaga {
  getArea() {
    return "Desenvolvimento Front-end";
  }
}
```

A classe Back-end retorna:

```text
Desenvolvimento Back-end
```

e a classe Full Stack retorna:

```text
Desenvolvimento Full Stack
```

O método é realmente utilizado na interface através de:

```javascript
resultado.vaga.getArea()
```

Por isso, o card consegue mostrar automaticamente a área correta da vaga.

Isso demonstra o uso de **herança e sobrescrita de métodos** dentro da aplicação.

---

# 🔄 Transformação do JSON em objetos

As vagas ficam armazenadas no arquivo:

```text
assets/data/vagas.json
```

Depois que o arquivo é carregado, os objetos do JSON são transformados em instâncias das classes.

O método:

```javascript
map()
```

é utilizado para percorrer as vagas.

Dependendo da categoria, é criada uma instância de `VagaFrontEnd`, `VagaBackEnd` ou `VagaFullStack`.

---

# 📦 Métodos de Array

O projeto utiliza diversos métodos de array.

Entre eles:

```javascript
map()
filter()
reduce()
forEach()
flatMap()
some()
```

### `map()`

Utilizado para:

- transformar dados do JSON em objetos;
- transformar elementos do formulário;
- gerar listas;
- analisar as vagas.

### `filter()`

Utilizado para:

- encontrar habilidades conhecidas;
- encontrar habilidades faltantes;
- filtrar vagas por categoria;
- encontrar vagas empatadas com a maior compatibilidade.

### `reduce()`

Utilizado para encontrar o maior percentual de compatibilidade.

### `forEach()`

Utilizado para percorrer listas e resultados.

### `flatMap()`

Utilizado para reunir as habilidades faltantes das vagas analisadas.

### `some()`

Utilizado para verificar se uma vaga pertence ao conjunto das melhores vagas.

---

# 🧠 Callback

O projeto utiliza callbacks em diferentes partes do código.

Um exemplo ocorre nos eventos:

```javascript
btnCandidato.addEventListener("click", () => {
  mostrarFormularioCandidato();
});
```

Métodos como `map()`, `filter()`, `reduce()` e `forEach()` também recebem funções de callback.

---

# 🔒 Closure

Foi criada uma closure para contar quantas análises foram realizadas durante a sessão.

```javascript
function criarContadorAnalises() {
  let quantidadeAnalises = 0;

  return function () {
    quantidadeAnalises++;

    return quantidadeAnalises;
  };
}
```

A função interna continua tendo acesso à variável `quantidadeAnalises` mesmo após a execução da função externa.

---

# 🌐 Carregamento das vagas com Fetch

As vagas são carregadas utilizando:

```javascript
fetch()
```

A função responsável utiliza:

```javascript
async
await
try
catch
response.ok
```

O projeto também trata explicitamente diferentes situações durante o carregamento.

## ⏳ Estado de carregamento

Antes da análise é exibida a mensagem:

```text
Carregando vagas...
```

## 📭 Estado vazio

Se o arquivo JSON for carregado corretamente, mas não possuir nenhuma vaga:

```javascript
[]
```

a aplicação apresenta:

```text
Nenhuma vaga disponível
```

## ❌ Estado de erro

Caso ocorra erro durante o carregamento, a função retorna:

```javascript
null
```

e a interface apresenta:

```text
Erro ao carregar as vagas
```

Essa diferença permite separar:

```text
[vagas...] → sucesso
[] → arquivo carregado, porém vazio
null → erro no carregamento
```

## 🔍 Nenhuma vaga compatível com a categoria

O arquivo pode possuir vagas normalmente, mas nenhuma delas corresponder ao filtro utilizado.

Nesse caso a aplicação apresenta:

```text
Nenhuma vaga encontrada
```

Essa situação é diferente de um erro de carregamento ou de um catálogo vazio.

---

# 💾 LocalStorage

O perfil do candidato é armazenado utilizando:

```javascript
localStorage
```

Antes de salvar o objeto:

```javascript
JSON.stringify()
```

é utilizado.

Para recuperar:

```javascript
JSON.parse()
```

A aplicação também trata a situação em que não existe nenhum perfil salvo e possui tratamento para dados inválidos armazenados no navegador.

---

# 🖥️ Manipulação do DOM

O formulário, mensagens e cards das vagas são criados dinamicamente pelo JavaScript.

Entre os recursos utilizados estão:

```javascript
innerHTML
document.createElement()
classList.add()
appendChild()
```

Os cards não ficam escritos diretamente no arquivo HTML.

---

# ♿ Acessibilidade

A aplicação possui recursos voltados para acessibilidade, como:

- HTML semântico;
- `lang="pt-BR"`;
- `label` associado aos inputs;
- `fieldset`;
- `legend`;
- `alt` na imagem;
- foco visível;
- `aria-label`;
- `aria-live`.

As mensagens dinâmicas utilizam:

```html
aria-live="polite"
```

---

# 🔎 SEO

O projeto possui recursos básicos de SEO.

```html
<title>
  CatchaTechJob | Compatibilidade com vagas de tecnologia
</title>
```

e:

```html
<meta
  name="description"
  content="Encontre vagas de tecnologia compatíveis com suas habilidades, experiência e área de atuação."
>
```

---

# 📱 Responsividade

A aplicação foi desenvolvida utilizando a abordagem **Mobile First**.

O layout utiliza **Flexbox** e não utiliza CSS Grid.

Também são utilizados:

```css
flex-wrap
gap
width: 100%
max-width: 100%
object-fit: cover
```

As principais media queries são:

```text
600px ou mais → tablet
1024px ou mais → desktop
```

---

# 🎨 Tema claro e escuro

A aplicação possui um botão **Alterar tema da página** que permite alternar entre os temas claro e escuro.

A preferência é salva no `localStorage`.

---

# 🌤️ Clima e Geolocalização

O projeto utiliza a API de geolocalização do navegador.

A localização é obtida através de:

```javascript
navigator.geolocation.getCurrentPosition()
```

Depois, latitude e longitude são utilizadas para consultar a API **Open-Meteo**.

A aplicação apresenta temperatura atual e condição climática.

Caso a localização não seja autorizada ou ocorra algum erro:

```text
Clima indisponível.
```

é apresentado ao usuário.

---

# 🛠️ Tecnologias utilizadas

- HTML5;
- CSS3;
- JavaScript;
- ES Modules;
- Fetch API;
- LocalStorage;
- Geolocation API;
- Open-Meteo API;
- Git;
- GitHub;
- Trello.

O projeto não utiliza:

- React;
- TypeScript;
- CSS Grid;
- back-end;
- banco de dados;
- jQuery;
- Axios.

---

# 📁 Estrutura do projeto

```text
CatchaTechJob/
│
├── index.html
├── README.md
│
└── assets/
    │
    ├── data/
    │   └── vagas.json
    │
    ├── img/
    │   └── Imagem de logo.jpg
    │
    ├── style/
    │   └── index.style.css
    │
    └── scripts/
        ├── main.js
        ├── motor.js
        ├── ui.js
        ├── dados.js
        ├── tema.js
        └── clima.js
```

---

# 📂 Responsabilidade dos módulos

## `main.js`

Responsável por controlar o fluxo principal da aplicação e conectar os demais módulos.

## `motor.js`

Responsável por:

- classes;
- herança;
- cálculo de compatibilidade;
- classificação;
- experiência;
- tratamento de empate;
- recomendação de estudos;
- closure do contador de análises.

## `ui.js`

Responsável por:

- formulário;
- cards;
- mensagens;
- resultados;
- manipulação visual do DOM.

## `dados.js`

Responsável por:

- `fetch` das vagas;
- tratamento de erros;
- LocalStorage;
- salvar e recuperar perfil.

## `tema.js`

Responsável pela troca e persistência dos temas claro e escuro.

## `clima.js`

Responsável pela geolocalização e consulta das informações meteorológicas.

---

# 🚀 Como executar

1. Clone o repositório ou faça o download do projeto.
2. Abra a pasta no Visual Studio Code.
3. Execute utilizando o **Live Server**.
4. Abra a página principal.
5. Clique em **Sou candidato**.
6. Preencha o formulário.
7. Escolha sua categoria.
8. Marque suas tecnologias.
9. Informe seu tempo de experiência.
10. Clique em **Encontrar vagas**.
11. Aguarde o carregamento.
12. Analise os resultados apresentados.

O Live Server é utilizado porque a aplicação carrega o arquivo `vagas.json` através de `fetch()`.

---

# 📋 Organização do projeto

O planejamento e acompanhamento das tarefas foram realizados através do Trello.

## Trello

https://trello.com/b/LMzJS6V4/projeto-catchatechjob

---

# 🎥 Vídeo de apresentação

(https://drive.google.com/file/d/10lPmdd5FTQ2a_KhBV4Udxe3HfYE8wdjU/view?usp=drive_link)

## Link do vídeo

Será adicionado após a gravação.

---

# 🤖 Uso de Inteligência Artificial

Durante o desenvolvimento do CatchaTechJob foram utilizadas ferramentas de Inteligência Artificial como apoio ao processo de estudo.

A IA foi utilizada principalmente para:

- revisar código;
- identificar erros;
- discutir possíveis soluções;
- explicar conceitos;
- revisar requisitos;
- auxiliar na acessibilidade;
- revisar a organização da aplicação;
- auxiliar na documentação.

As sugestões recebidas não foram utilizadas automaticamente.

Elas foram analisadas, testadas e adaptadas antes de serem adicionadas ao projeto.

Durante o desenvolvimento também foram realizadas revisões para entender o funcionamento das soluções implementadas.

O uso de Inteligência Artificial neste projeto teve como objetivo auxiliar o processo de aprendizado e desenvolvimento, sem substituir a compreensão dos conteúdos estudados.

---

# 🚧 Limitações atuais

A versão atual do CatchaTechJob é uma aplicação exclusivamente Front-End.

Por isso:

- não possui autenticação;
- não possui servidor próprio;
- não possui banco de dados;
- as vagas são carregadas de um arquivo JSON;
- o perfil é armazenado apenas no navegador;
- empresas ainda não podem cadastrar vagas.

---

# 🏢 Área para empresas

A aplicação possui o botão **Empresa**.

Essa área será utilizada inicialmente para apresentar uma página informando que a funcionalidade está **Em construção**.

A ideia é manter esse espaço preparado para uma evolução futura do projeto.

Uma versão posterior poderia permitir que empresas:

- realizassem cadastro;
- acessassem uma área própria;
- registrassem vagas;
- alterassem vagas;
- removessem vagas;
- acompanhassem oportunidades cadastradas.

Para isso, seria necessário adicionar tecnologias que estão fora do escopo atual do projeto, como:

- back-end;
- servidor;
- API própria;
- banco de dados;
- SQL;
- autenticação.

A arquitetura atual também precisaria ser adaptada.

Hoje o fluxo é direcionado principalmente ao candidato:

```text
Candidato
   ↓
Formulário
   ↓
Perfil
   ↓
Vagas do JSON
   ↓
Motor de compatibilidade
   ↓
Resultados
```

Com empresas cadastrando vagas, a origem dos dados deixaria de ser somente o arquivo `vagas.json`.

Também seria necessário revisar:

- estrutura das vagas;
- validações;
- persistência;
- formulários;
- comunicação com o servidor;
- lógica de cadastro;
- partes do fluxo atual do candidato.

Essa funcionalidade fica registrada como uma possível evolução do CatchaTechJob após o estudo de conteúdos relacionados a back-end e bancos de dados.

---

# 🔮 Melhorias futuras

Algumas possíveis evoluções do projeto são:

- autenticação;
- cadastro de usuários;
- cadastro de empresas;
- cadastro real de vagas;
- banco de dados;
- API própria;
- integração com SQL;
- favoritos;
- filtros por modalidade;
- filtros por salário;
- histórico de análises;
- painel do candidato;
- painel da empresa;
- novos critérios de desempate;
- novos critérios de compatibilidade;
- melhorias visuais;
- deploy da aplicação.

---

# 📌 Status do projeto

✅ Aplicação acadêmica funcional.

Os principais requisitos da versão atual foram implementados.

O projeto pode continuar recebendo melhorias depois da conclusão da versão utilizada para avaliação.

---

# 📚 Principais aprendizados

Durante o desenvolvimento foram trabalhados:

- organização de projetos;
- HTML semântico;
- CSS;
- Flexbox;
- responsividade;
- JavaScript;
- arrays;
- objetos;
- métodos de array;
- Programação Orientada a Objetos;
- classes;
- herança;
- sobrescrita de métodos;
- callbacks;
- closures;
- Promises;
- async/await;
- Fetch API;
- LocalStorage;
- manipulação do DOM;
- eventos;
- validação;
- tratamento de erros;
- acessibilidade;
- SEO;
- APIs do navegador;
- Git;
- GitHub;
- Kanban.

---

## 👨‍🎓 Projeto acadêmico

Projeto desenvolvido como atividade de estudo e avaliação durante a formação em Desenvolvimento Front-End.

O objetivo principal foi reunir os conteúdos estudados durante o módulo em uma aplicação funcional, organizada e que pudesse ser explicada durante a apresentação do projeto.
