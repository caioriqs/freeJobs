> Especialista Digital Analytics: Caio Gomes<br />
> Documento de Especificação Técnica - Atacadão

<br />

## Implementação da Camada de dados
Última atualização: 19/04/2020<br />
Em caso de dúvidas, entrar em contato com: [silva.caiohenrique@gmail.com](mailto:silva.caiohenrique@gmail.com)

<br />

## Índice
- [Objetivo](#objetivo)
- [Overview e Descrições Técnicas](#overview-e-descrições-técnicas)
- [Especificação de Micro-conversões](#especificação-de-micro-conversões)
- [Especificação de Conversões](#especificação-de-conversões)
- [Considerações Finais](#considerações-finais)

<br />

## Objetivo
Este documento tem como objetivo instruir a implementação do Google Tag Manager, da camada de dados e de data attributes para utilização de recursos de monitoramento do Google Analytics referentes ao ambiente do site Atacadão.

<br />

## Overview e Descrições Técnicas



### Camada de dados (DataLayer)

> É um array de objetos javascript utilizado pelo Google Tag Manager para receber em seus atributos, dados importantes do site.
Para implementar o dataLayer no site, o desenvolvedor pode utilizar formas diferentes para preencher os dados. Essas formas são dependentes da ação estabelecida na documentação e também do nível da interação.

**Instalação**<br />
Inserir a camada de dados antes do snippet de instalação do Google Tag Manager. Exemplo:

```html
<script>
	window.dataLayer = window.dataLayer || [];
	window.dataLayer = [{
		'atributo1': '[[valor1]]',
		'atributo2': '[[valor2]]'
	}];
</script>
```

OU

```html
<script>
	window.dataLayer = window.dataLayer || [];
	window.dataLayer.push({
		'atributo1': '[[valor1]]',
		'atributo2': '[[valor2]]'
	});
</script>
```

<br />	 	

## Implementação

A documentação foi descrita para algumas áreas especificas do ambiente Atacadão.


### Especificações Globais:

**Itens Gerais:**<br />
Todas as informações entre colchetes `[[  ]]` são variáveis dinâmicas que devem ser preenchidas com seus respectivos valores; <br />
Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais; <br />
Caso a informação solicitada não estiver disponível retornar 'nao_disponivel'. - Mudar de acordo com o projeto

---

<br />

### Especificação de Micro-conversões:


**1 - Clique no Menu principal:**<br />

- **Quando:** Ao clicar em qualquer item do menu;
- **Onde:** Menu principal;

```html
dataLayer.push({
		'event': 'event',
		'eventCategory': 'site:home',
		'eventAction': 'clique:menu-principal',
		'eventLabel': 'opcao:[item-menu]'
	});
```

| Variável 			| Exemplo 											| Descrição				|
| :----------------	| :------------------------------------------------	| :-------------------	|
| [item-menu]		| 'home', 'como-participar', 'meus-numeros'	e etc	| Nome do item no Menu	|

<br />


**2 - Clique no Menu lateral:**<br />

- **Quando:** Ao clicar em qualquer item do menu;
- **Onde:** Menu lateral;

```html
dataLayer.push({
		'event': 'event',
		'eventCategory': 'site:home',
		'eventAction': 'clique:menu-lateral',
		'eventLabel': 'opcao:[item-menu]'
	});
```

| Variável 			| Exemplo 											| Descrição				|
| :----------------	| :------------------------------------------------	| :-------------------	|
| [item-menu]		| 'home', 'como-participar', 'meus-numeros'	e etc	| Nome do item no Menu	|

<br />

**3 - Clique nas Redes Sociais:**<br />

- **Quando:** Ao clicar em qualquer Rede Social;
- **Onde:** Menu lateral;

```html
dataLayer.push({
		'event': 'event',
		'eventCategory': 'site:home',
		'eventAction': 'clique:menu-lateral:redes-sociais',
		'eventLabel': 'social:[rede-social]'
	});
```

| Variável 			| Exemplo 						| Descrição				|
| :----------------	| :----------------------------	| :-------------------	|
| [rede-social]		| 'facebook', 'twitter'	e etc	| Nome da Rede Social	|

<br />

**4 - Clique Login:**<br />

- **Quando:** Ao clicar em Entrar;
- **Onde:** Menu;

```html
dataLayer.push({
		'event': 'event',
		'eventCategory': 'site:home',
		'eventAction': 'clique:login',
		'eventLabel': 'login:entrar'
	});
```

<br />

**5 - Sucesso Login:**<br />

- **Quando:** No callback de login;
- **Onde:** Ambiente de Login;

```html
dataLayer.push({
		'event': 'event',
		'eventCategory': 'site:login',
		'eventAction': 'clique:entrar',
		'eventLabel': 'tentativa:[erro/sucesso]'
	});
```

| Variável 			| Exemplo 				| Descrição				|
| :----------------	| :-------------------	| :-------------------	|
| [erro/sucesso]	| 'erro' ou 'sucesso'	| Status de tantativa	|

<br />

**6 - Erro = Sem Cadastro:**<br />

- **Onde:** No callback de erro;
- **Quando:** Na mensagem de erro de "sem cadastro";

```html
dataLayer.push({
		'event': 'event',
		'eventCategory': 'site:login',
		'eventAction': 'cadastro:mensagem',
		'eventLabel': 'sem-cadastro'
	});
```

<br />

**7 - Tentar outro CPF/CNPJ:**<br />

- **Onde:** Tela de Cadastro;
- **Quando:** Na mensagem de erro de "sem cadastro";

```html
dataLayer.push({
		'event': 'event',
		'eventCategory': 'site:login',
		'eventAction': 'clique:link-entrar',
		'eventLabel': 'tentar-outro-cpf-ou-cnpj'
	});
```

<br />


**8 - Cadastro de Cliente:**<br />

- **Onde:** Tela de Cadastro;
- **Quando:** Quando o cliente escolher por onde quer se cadastrar;

```html
dataLayer.push({
		'event': 'event',
		'eventCategory': 'site:cadastro',
		'eventAction': 'clique:cadastrar',
		'eventLabel': 'opcao:[item-selecionado]'
	});
```

| Variável 				| Exemplo 							| Descrição				|
| :------------------	| :------------------------------	| :-------------------	|
| [item-selecionado]	| 'facebook', 'google' ou 'email'	| Opção selecionada		|

<br />

**9 - Banner - Vem Participar:**<br />

- **Onde:** Banner Principal;
- **Quando:** Quando o cliente clicar para participar;

```html
dataLayer.push({
		'event': 'event',
		'eventCategory': 'site:home',
		'eventAction': 'clique:banner',
		'eventLabel': 'vem-dinheirao:participar'
	});
```

<br />

**10 - Banner - Link Vídeo:**<br />

- **Onde:** Banner Principal;
- **Quando:** Quando o cliente clicar no link do video da campanha;

```html
dataLayer.push({
		'event': 'event',
		'eventCategory': 'site:home',
		'eventAction': 'clique:banner',
		'eventLabel': 'vem-dinheirao:video-campanha'
	});
```

<br />

**11 - Como Participar:**<br />

- **Onde:** Como Participar;
- **Quando:** Quando o cliente clicar no link de cadastro;

```html
dataLayer.push({
		'event': 'event',
		'eventCategory': 'site:home',
		'eventAction': 'clique:como-participar',
		'eventLabel': 'cadastre-aqui'
	});
```

<br />

**12 - Ganhadores:**<br />

- **Onde:** Ganhadores;
- **Quando:** Quando o cliente clicar no link de ganhadores;

```html
dataLayer.push({
		'event': 'event',
		'eventCategory': 'site:home',
		'eventAction': 'clique:ganhadores',
		'eventLabel': 'conheca-ganhadores'
	});
```

<br />

**13 - Scroll:**<br />

- **Quando:** Ao "rolar" a página para baixo;
- **Obs:** o evento deve ser disparado uma única vez por página

```html
dataLayer.push({
		'event': 'scroll',
		'eventCategory': 'site:home',
		'eventAction': 'scroll',
		'eventLabel': '[scroll-percent]'
	});
```

| Variável 			| Exemplo 					| Descrição															|
| :----------------	| :------------------------	| :---------------------------------------------------------------	|
| [scroll-percent]	| '25', '50', '75' e '100'	| retornar a porcentagem da tela que o cliente "rolou" para baixo	|

<br />

---

### Especificação de Conversões:

**Sucesso Cadastro Cliente:**<br />

- **Onde:** No callback de sucesso .

```html
<script>
	dataLayer.push({
		'event': 'conversion',
		'eventCategory': 'site:cadastro',
		'eventAction': 'sucesso',
		'eventLabel' : 'cliente-cadastrado'
	});
</script>
```

<br />

**Sucesso Cadastrar Nota:**<br />

- **Onde:** No callback de sucesso .

```html
<script>
	dataLayer.push({
		'event': 'conversion',
		'eventCategory': 'site:notas',
		'eventAction': 'sucesso',
		'eventLabel' : 'nota-cadastrada
	});
</script>
```

<br />

---

<br />

## Considerações Finais:

> Link de referência: [Documentação Oficial Google Tag Manager](https://developers.google.com/tag-manager/quickstart)
