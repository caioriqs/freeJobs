> Especialista Digital Analytics: Caio Gomes<br />
> Documento de Especificação Técnica - Ibby's T-Shirt

<br />

## Implementação da Camada de dados
Última atualização: 05/04/2022<br />
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
Este documento tem como objetivo instruir a implementação do Google Tag Manager, da camada de dados e de data attributes para utilização de recursos de monitoramento do Google Analytics referentes ao ambiente de [Ibby's T-Shirt](https://enhancedecommerce.appspot.com/).

<br />

## Overview e Descrições Técnicas

### Instalação do Google Tag Manager

> Para instalar o Google Tag Manager no seu site, basta seguir os seguintes passos: 

**Dentro do "head"**<br />
Cole esse código o mais alto possível na tag *head* da página:

```html
<!-- Google Tag Manager -->
<script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
})(window,document,'script','dataLayer','GTM-P5GM26N');</script>
<!-- End Google Tag Manager -->
```
<br />

**Início do "body"**<br />
Além disso, cole esse código imediatamente após a tag de abertura *body*:

```html
<!-- Google Tag Manager (noscript) -->
<noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-P5GM26N"
height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
<!-- End Google Tag Manager (noscript) -->
```

<br />

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

### Atributos HTML (Data Attributes)

> São atributos customizados inseridos nos elementos HTML da página que permite a inclusão de dados adicionais.

**Instalação**
1. Elementos de link: ```<a href="..." class="minha_classe">Link</a>``` <br />
Elementos do tipo link que foram mapeados, precisam receber a classe **gtm-link-event** e os data attributes em sua estrutura.

```html
<a href="http://www.meudominio.com.br/page2"
	class="minha_classe gtm-link-event"
 	gtm-event-data-category="[[exemplo:valor-categoria]]"
  	gtm-event-data-action="[[exemplo:valor-acao]]"
  	gtm-event-data-label="[[exemplo:valor-rotulo]]">Texto do link</a>
```

2. Elementos comuns: ```<div class="minha_classe">Elemento</div>``` <br />
Todos os elementos comuns do html que não são links e que foram mapeados, precisam receber a classe **gtm-element-event** em sua estrutura.

```html
<div 	class="minha_classe gtm-element-event"
  	gtm-event-data-category="[[exemplo:valor-categoria]]"
 	gtm-event-data-action="[[exemplo:valor-acao]]"
 	gtm-event-data-label="[[exemplo:valor-rotulo]]">Texto do elemento</div>
```

#### Importante:
> Todos os links e botões citados nesta documentação devem ter em sua estrutura `html` a classe `gtm-link-event` se for um link `<a>` ou `gtm-element-event` se o elemento não for um link `<a>` conforme demonstraremos nos exemplos específicos.<br />

> Devem ter também os data-attributes `gtm-event-data-category`, `gtm-event-data-action` e `gtm-event-data-label` preenchidos conforme instruções específicas.

<br />	 	

## Implementação

A documentação foi descrita para algumas áreas especificas do ambiente [Ibby's T-Shirt](https://enhancedecommerce.appspot.com/).


### Especificações Globais:

**Itens Gerais:**<br />
Todas as informações entre colchetes `[[  ]]` são variáveis dinâmicas que devem ser preenchidas com seus respectivos valores; <br />
Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais; <br />
Caso a informação solicitada não estiver disponível retornar 'nao_disponivel'. - Mudar de acordo com o projeto

---

<br />

### Especificação de Micro-conversões:


**1 - Clique em Informações do Produto:**<br />

- **Quando:** Ao clicar em qualquer produto, no ícono de informação "i" (canto superior direito da imagem da camiseta);
- **Onde:** Lista de Produtos;

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	gtm-event-data-category="home:lista-produtos"
	gtm-event-data-action="clique:informacoes"
	gtm-event-data-label="camiseta:[[nome camiseta]]"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	gtm-event-data-category="home:lista-produtos"
	gtm-event-data-action="clique:informacoes"
	gtm-event-data-label="camiseta:[[nome camiseta]]"
>Botão</i>
```

| Variável 			| Exemplo 											| Descrição			|
| :----------------	| :------------------------------------------------	| :---------------	|
| [[nome camiseta]]	| 'compton t-shirt', 'flexigen t-shirt' e etc		| Nome do item  	|

<br />

### Product Impression:

- **Onde:** O objeto javascript (dataLayer) abaixo deve ser disparado uma única vez no carregamento de uma página de lista de produtos.

```html
<script>
dataLayer.push({
	'event': 'productImpression',
	'eventCategory': 'ecommerce',
	'eventAction': 'view_item'
	'ecommerce': {
		'impressions': [{
			'name': '[[nome-produto]]',				//Nome ou ID do produto é obrigatório
			'id': '[[id-produto]]',
			'price': '[[preco-produto]]',
			'brand': '[[marca-produto]]',
			'category': '[[categoria-produto]]',
			'variant': '[[variacao-produto]]', 		//tamanho - cor
			'list': '[[lista-produto]]',
			'position': '[[posicao-produto]]'
		}]
	}
});
</script>
```

<br />

| Nome 			| Variável 					| Exemplo 					| Descrição 								|
| :------------	| :------------------------ | :------------------------ | :---------------------------------------- |
| name 			| [[nome-produto]] 			| 'compton t-shirt' 		| Nome do produto 							|
| id			| [[id-produto]] 			| '323qe12'					| ID do produto 							|
| price			| [[preco-produto]] 		| '44.00' 					| Preço do produto							|
| brand 		| [[marca-produto]] 		| 'compton'					| Marca do produto 	 						|
| category 		| [[categoria-produto]] 	| 'camiseta'				| Categoria do produto 						|
| variant 		| [[variacao-produto]] 		| 'g - amarelo'				| Variação do produto (tamanho - cor)		|
| list 	 		| [[lista-produto]] 		| 'camisetas'				| Nome da lista de produtos 				|
| position 		| [[posicao-produto]] 		| '1'						| Posição que o produto aparece na lista 	|

<br />

### Product Click:

- **Onde:** O objeto javascript (dataLayer) abaixo deve ser disparado uma única vez no clique em algum produto.

```html
<script>
dataLayer.push({
	'event': 'productClick',
	'eventCategory': 'ecommerce',
	'eventAction': 'click_item'
	'ecommerce': {
		'click': {
			'actionField': {'list': '[[lista-produto]]'},
			'products': [{
				'name': '[[nome-produto]]',				//Nome ou ID do produto é obrigatório
				'id': '[[id-produto]]',
				'price': '[[preco-produto]]',
				'brand': '[[marca-produto]]',
				'category': '[[categoria-produto]]',
				'variant': '[[variacao-produto]]',
				'position': '[[posicao-produto]]'
			}]
		}
	}
});
</script>
```

<br />

| Nome 			| Variável 					| Exemplo 					| Descrição 								|
| :------------	| :------------------------ | :------------------------ | :---------------------------------------- |
| name 			| [[nome-produto]] 			| 'compton t-shirt' 		| Nome do produto 							|
| id			| [[id-produto]] 			| '323qe12'					| ID do produto 							|
| price			| [[preco-produto]] 		| '44.00' 					| Preço do produto							|
| brand 		| [[marca-produto]] 		| 'compton'					| Marca do produto 	 						|
| category 		| [[categoria-produto]] 	| 'camiseta'				| Categoria do produto 						|
| variant 		| [[variacao-produto]] 		| 'g - amarelo'				| Variação do produto (tamanho - cor)		|
| list 	 		| [[lista-produto]] 		| 'camisetas'				| Nome da lista de produtos 				|
| position 		| [[posicao-produto]] 		| '1'						| Posição que o produto aparece na lista 	|

<br />

### Product Detail:

- **Onde:** O objeto javascript (dataLayer) abaixo deve ser disparado uma única vez no carregamento da página de um produto.

```html
<script>
dataLayer.push({
	'event': 'productDetail',
	'eventCategory': 'ecommerce',
	'eventAction': 'detail_item'
	'ecommerce': {
		'detail': {
			'actionField': {'list': '[[lista-produto]]'},
			'products': [{
				'name': '[[nome-produto]]',				//Nome ou ID do produto é obrigatório
				'id': '[[id-produto]]',
				'price': '[[preco-produto]]',
				'brand': '[[marca-produto]]',
				'category': '[[categoria-produto]]',
				'variant': '[[variacao-produto]]'
			}]
		}
	}

});
</script>
```

<br />

| Nome 			| Variável 					| Exemplo 					| Descrição 								|
| :------------	| :------------------------ | :------------------------ | :---------------------------------------- |
| name 			| [[nome-produto]] 			| 'compton t-shirt' 		| Nome do produto 							|
| id			| [[id-produto]] 			| '323qe12'					| ID do produto 							|
| price			| [[preco-produto]] 		| '44.00' 					| Preço do produto							|
| brand 		| [[marca-produto]] 		| 'compton'					| Marca do produto 	 						|
| category 		| [[categoria-produto]] 	| 'camiseta'				| Categoria do produto 						|
| variant 		| [[variacao-produto]] 		| 'g - amarelo'				| Variação do produto (tamanho - cor)		|

<br />

### AddToCart:

- **Onde:** O objeto javascript (dataLayer) abaixo deve ser disparado uma única vez no clique do CTA de adição de produto ao carrinho.

```html
<script>
dataLayer.push({
	'event': 'addToCart',
	'eventCategory': 'ecommerce',
	'eventAction': 'addToCart'
	'ecommerce': {
		'add': {
			'products': [{
				'name': '[[nome-produto]]',				//Nome ou ID do produto é obrigatório
				'id': '[[id-produto]]',
				'price': '[[preco-produto]]',
				'brand': '[[marca-produto]]',
				'category': '[[categoria-produto]]',
				'variant': '[[variacao-produto]]',
				'quantity': '[[quantidade-produto]]'
			}]
		}
	}
});
</script>
```

<br />

| Nome 			| Variável 					| Exemplo 					| Descrição 								|
| :------------	| :------------------------ | :------------------------ | :---------------------------------------- |
| name 			| [[nome-produto]] 			| 'compton t-shirt' 		| Nome do produto 							|
| id			| [[id-produto]] 			| '323qe12'					| ID do produto 							|
| price			| [[preco-produto]] 		| '44.00' 					| Preço do produto							|
| brand 		| [[marca-produto]] 		| 'compton'					| Marca do produto 	 						|
| category 		| [[categoria-produto]] 	| 'camiseta'				| Categoria do produto 						|
| variant 		| [[variacao-produto]] 		| 'g - amarelo'				| Variação do produto (tamanho - cor)		|
| quantity 		| [[quantidade]] 			| '2'						| Quantidade de produtos 				|

<br />

### Remove From Cart:

- **Onde:** O objeto javascript (dataLayer) abaixo deve ser disparado uma única vez no clique do botão para remover um produto do carrinho.

```html
<script>
dataLayer.push({
	'event': 'removeFromCart',
	'eventCategory': 'ecommerce',
	'eventAction': 'removeFromCart'
	'ecommerce': {
		'remove': {
			'products': [{
				'name': '[[nome-produto]]',				//Nome ou ID do produto é obrigatório
				'id': '[[id-produto]]',
				'price': '[[preco-produto]]',
				'brand': '[[marca-produto]]',
				'category': '[[categoria-produto]]',
				'variant': '[[variacao-produto]]',
				'quantity': '[[quantidade-produto]]'
			}]
		}
	}
});
</script>
```

<br />

| Nome 			| Variável 					| Exemplo 					| Descrição 								|
| :------------	| :------------------------ | :------------------------ | :---------------------------------------- |
| name 			| [[nome-produto]] 			| 'compton t-shirt' 		| Nome do produto 							|
| id			| [[id-produto]] 			| '323qe12'					| ID do produto 							|
| price			| [[preco-produto]] 		| '44.00' 					| Preço do produto							|
| brand 		| [[marca-produto]] 		| 'compton'					| Marca do produto 	 						|
| category 		| [[categoria-produto]] 	| 'camiseta'				| Categoria do produto 						|
| variant 		| [[variacao-produto]] 		| 'g - amarelo'				| Variação do produto (tamanho - cor)		|
| quantity 		| [[quantidade]] 			| '2'						| Quantidade de produtos 				|

<br />

### Promotion Impression:

- **Onde:** O objeto javascript (dataLayer) abaixo deve ser disparado uma única vez na visualização de um banner.

```html
<script>
dataLayer.push({
	'event': 'promotionImpression',
	'eventCategory': 'ecommerce',
	'eventAction': 'promotion_view'
	'ecommerce': {
		'promoView': {
			'promotions': [{
				'id': '[[id-banner]]',				//Nome ou ID do banner é obrigatório
				'name': '[[nome-banner]]',
				'creative': '[[arte-banner]]',
				'position': '[[posicao-banner]]'
			}]
		}
	}
});
</script>
```

<br />

---

### Especificação de Conversões:

**Sucesso Compra:**<br />

- **Onde:** No callback de sucesso;

```html
<script>
	dataLayer.push({
		'event': 'conversion',
		'eventCategory': 'ecommerce',
		'eventAction': 'sucesso:compra'
	});
</script>
```

<br />

### Checkout:

****<br />

- **Onde:** O objeto javascript (dataLayer) abaixo deve ser disparado uma única vez no carregamento da páginas página de checkout.

```html
<script>
dataLayer.push({
	'event': 'checkout',
	'eventCategory': 'ecommerce',
	'eventAction': 'checkout_progress'
	'ecommerce': {
		'checkout': {
			'actionField': {'step': '[[passo-checkout]]'},
			'products': [{
				'name': '[[nome-produto]]',				//Nome ou ID do produto é obrigatório
				'id': '[[id-produto]]',
				'price': '[[preco-produto]]',
				'brand': '[[marca-produto]]',
				'category': '[[categoria-produto]]',
				'variant': '[[variacao-produto]]',
				'quantity': '[[quantidade-produto]]'
			}]
		}
	}
});
</script>
```

<br />

| Nome 			| Variável 					| Exemplo 								| Descrição 							|
| :------------	| :------------------------ | :-----------------------------------  | :----------------------------			|
| actionField 	| [[passo-checkout]]		| 'start', 'shipping', 'payment' e etc	| Passo atual do checkout 	 			|
| name 			| [[nome-produto]] 			| 'compton t-shirt' 					| Nome do produto 						|
| id			| [[id-produto]] 			| '323qe12'								| ID do produto 						|
| price			| [[preco-produto]] 		| '44.00' 								| Preço do produto						|
| brand 		| [[marca-produto]] 		| 'compton'								| Marca do produto 	 					|
| category 		| [[categoria-produto]] 	| 'camiseta'							| Categoria do produto 					|
| variant 		| [[variacao-produto]] 		| 'g - amarelo'							| Variação do produto (tamanho - cor)	|
| quantity 		| [[quantidade]] 			| '2'									| Quantidade de produtos 				|


<br />

### Purchase:

- **Onde:** O objeto javascript (dataLayer) abaixo deve ser disparado uma única vez no carregamento da página de transação, e se o usuário acessar novamente o link ou atualizar a página, o objeto não deve ser disparado novamente.

```html
<script>
dataLayer.push({
	'event': 'purchase',
	'eventCategory': '',
	'eventAction': '',
	'eventLabel': '',
	'ecommerce': {
		'purchase': {
			'actionField': {
				'id': '[[id-transacao]]',				//ID da transação é obrigatório
				'affiliation': '[[loja-transacao]]',
				'revenue': '[[valor-total-transacao]]',
				'tax': '[[taxa-transacao]]',
				'shipping': '[[frete-transacao]]',
				'coupon': '[[cupom-transacao]]'
			},
			'products': [{
				'name': '[[nome-produto]]',				//Nome ou ID do produto é obrigatório
				'id': '[[id-produto]]',
				'price': '[[preco-produto]]',
				'brand': '[[marca-produto]]',
				'category': '[[categoria-produto]]',
				'variant': '[[variacao-produto]]',
				'quantity': '[[quantidade-produto]]',
				'coupon': '[[cupom-produto]]'
			}]
		}
	}
});
</script>
```

*Descrição Purchase:*

| Nome 			| Variável 					| Exemplo 			| Descrição 										|
| :------------	| :------------------------	| :----------------	| :------------------------------------------------	|
| id 			| [[id-transacao]] 			| '298213890' 		| ID da Transação									|
| affiliation	| [[loja-transacao]] 		| 'xpto' 			| Loja que ocorreu a transação 						|
| revenue 		| [[valor-total-transacao]] | '85.50' 			| Valor total da transação incluindo frete e taxas	|
| tax 	 		| [[taxa-transacao]] 		| '1.00' 			| Taxas da transação 	 							|
| shipping 		| [[frete-transacao]] 		| '4.50' 			| Frete da transação 								|
| coupon 		| [[cupom-transacao]]		| 'ibbys10off'			| Cupom de desconto usado na transação				|

<br />

*Descrição Produtos:*

| Nome 			| Variável 					| Exemplo 					| Descrição 							|
| :------------	| :------------------------	| :------------------------ | :------------------------------------	|
| name 			| [[nome-produto]] 			| 'compton t-shirt' 		| Nome do produto 						|
| id			| [[id-produto]] 			| '323qe12'					| ID do produto 						|
| price			| [[preco-produto]] 		| '44.00' 					| Preço do produto						|
| brand 		| [[marca-produto]] 		| 'compton'					| Marca do produto 	 					|
| category 		| [[categoria-produto]] 	| 'camiseta'				| Categoria do produto 					|
| variant 		| [[variacao-produto]] 		| 'g - amarelo'				| Variação do produto (tamanho - cor)	|
| quantity 		| [[quantidade]] 			| '2'						| Quantidade de produtos 				|
| coupon		| [[cupom-produto]]	 		| 'ibbys10off'					| Cupom de desconto usado no produto	|

<br />

<br />

## Considerações Finais:

> Link de referência: [Documentação Oficial Google Tag Manager](https://developers.google.com/tag-manager/quickstart)
