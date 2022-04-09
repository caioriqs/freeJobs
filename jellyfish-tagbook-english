> Digital Analytics Specialist: Caio Gomes<br />
> Technical documentation - Ibby's T-Shirt

<br />

## Data Layer Implementation
Last Update: 08/04/2022<br />
In case of doubt, contact: [silva.caiohenrique@gmail.com](mailto:silva.caiohenrique@gmail.com)

<br />

## Índice
- [General Objective](#Goals)
- [Overview e Descrições Técnicas](#overview-e-descrições-técnicas)
- [Especificação de Micro-conversões](#especificação-de-micro-conversões)
- [Especificação de Conversões](#especificação-de-conversões)
- [Considerações Finais](#considerações-finais)

<br />

## Objetivo
This document aims to instruct the implementation of Google Tag Manager, the data layer and data attributes to use Google Analytics monitoring resources related to the [Ibby's T-Shirt](https://enhancedecommerce.appspot.com/).

<br />

## Overview and Technical Descriptions

### Google Tag Manager Setup

> To install Google Tag Manager on your website, just follow these steps: 

**Inside tag "head"**<br />
Paste this code as high as possible into the *head* tag of the page:

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

**Start "body" tag**<br />
Also, paste this code immediately after the opening *body* tag:

```html
<!-- Google Tag Manager (noscript) -->
<noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-P5GM26N"
height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
<!-- End Google Tag Manager (noscript) -->
```

<br />

### DataLayer

> It is an array of javascript objects used by Google Tag Manager to receive important site data in its attributes.
To implement the dataLayer on the website, the developer can use different ways to fill in the data. These forms are dependent on the action established in the documentation and also on the level of interaction.

**Install**<br />
Insert the data layer before the Google Tag Manager install snippet. Example:

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

### Data Attributes HTML

> They are custom attributes inserted in the HTML elements of the page that allow the inclusion of additional data.

**Setup**
1. Link element: ```<a href="..." class="minha_classe">Link</a>``` <br />
Link elements that have been mapped must receive the **gtm-link-event** class and the data attributes in their structure.

```html
<a href="http://www.meudominio.com.br/page2"
	class="minha_classe gtm-link-event"
 	gtm-event-data-category="[[Exemple:valor-categoria]]"
  	gtm-event-data-action="[[Exemple:valor-acao]]"
  	gtm-event-data-label="[[Exemple:valor-rotulo]]">Texto do link</a>
```

2. Common elements: ```<div class="minha_classe">Elemento</div>``` <br />
All common html elements that are not links and that have been mapped need to receive the **gtm-element-event** class in their structure.

```html
<div 	class="minha_classe gtm-element-event"
  	gtm-event-data-category="[[Exemple:valor-categoria]]"
 	gtm-event-data-action="[[Exemple:valor-acao]]"
 	gtm-event-data-label="[[Exemple:valor-rotulo]]">Texto do elemento</div>
```

#### Important:
> All links and buttons mentioned in this documentation must have in their `html` structure the `gtm-link-event` class if it is a `<a>` link or `gtm-element-event` if the element is not a link ` <a>` as we will demonstrate in the specific examples.<br />

> They must also have the `gtm-event-data-category`, `gtm-event-data-action` and `gtm-event-data-label` data-attributes filled according to specific instructions.

<br />	 	

## Implementation

Documentation has been described for some specific areas of the environment [Ibby's T-Shirt](https://enhancedecommerce.appspot.com/).


### Global Specifications:

**Itens Gerais:**<br />
All information enclosed in square brackets `[[ ]]` are dynamic variables that must be filled with their respective values; <br />
All values sent to Google Analytics must be sanitized, that is, without spaces, accents or special characters; <br />
If the requested information is not available, return 'not_available'. - Change according to the project

---

<br />

### Micro-conversions specification:


**1 - Click on Product Information:**<br />

- **When:** When clicking on any product, on the information icon "i" (upper right corner of the t-shirt image);
- **Where:** Product list;

```html
<!-- Use if element is a link -->
<a href="#"
	class="gtm-link-event"
	gtm-event-data-category="home:product-lists"
	gtm-event-data-action="click:informacoes"
	gtm-event-data-label="t-shirt:[[t-shirt name]]"
>Link</a>

<!-- Use if element is not a link -->
<i 	class="gtm-element-event"
	gtm-event-data-category="home:product-lists"
	gtm-event-data-action="click:informacoes"
	gtm-event-data-label="t-shirt:[[t-shirt name]]"
>Botão</i>
```

| Variable 			| Exemple 											| Description		|
| :----------------	| :------------------------------------------------	| :---------------	|
| [[Name t-shirt]]	| 'compton t-shirt', 'flexigen t-shirt' e etc		| Name do item  	|

<br />

**2 - Click Mini-Basket:**<br />

- **When:** When interacting with the Mini-Basket;
- **Where:** Right side on screen;

```html
<!-- Use if element is a link -->
<a href="#"
	class="gtm-link-event"
	gtm-event-data-category="[[page]]:mini-basket"
	gtm-event-data-action="'click:t-shirt' or 'click:checkout'"
	gtm-event-data-label="[[item]]"
>Link</a>

<!-- Use if element is not a link -->
<i 	class="gtm-element-event"
	gtm-event-data-category="[[page]]:mini-basket"
	gtm-event-data-action="Click:[[item]] or [[checkout]]"
	gtm-event-data-label="[[item]]"
>Botão</i>
```

| Variable 			| Exemple 											| Description			|
| :----------------	| :--------------------------------------------		| :---------------		|
| [[page]]			| 'home', 'detail_item' e etc						| Interaction page  	|
| [[item]]			| 'compton t-shirt', 'flexigen t-shirt' e etc		| Item name  			|


<br />

### Product Impression:

- **Where:** The javascript object (dataLayer) below must be fired once when a product list page is loaded.

```html
<script>
dataLayer.push({
	'event': 'productImpression',
	'eventCategory': 'ecommerce',
	'eventAction': 'view_item'
	'ecommerce': {
		'impressions': [{
			'name': '[[product-name]]',				//Product name or ID is required
			'id': '[[product-id]]',
			'price': '[[product-price]]',
			'brand': '[[product-brand]]',
			'category': '[[product-category]]',
			'variant': '[[product-variant]]', 		//size - collor
			'list': '[[product-list]]',
			'position': '[[product-position]]'
		}]
	}
});
</script>
```

<br />

| Name 			| Variable 					| Exemple 					| Description 								|
| :------------	| :------------------------ | :------------------------ | :---------------------------------------- |
| name 			| [[product-name]] 			| 'compton t-shirt' 		| Product Name 								|
| id			| [[product-id]] 			| '323qe12'					| Product ID 								|
| price			| [[product-price]] 		| '44.00' 					| Product Price								|
| brand 		| [[product-brand]] 		| 'compton'					| Product Brand 	 						|
| category 		| [[product-category]] 		| 't-shirt'					| Procuct Category 							|
| variant 		| [[product-variant]] 		| 'g - amarelo'				| Procuct Variant (size - collor)			|
| list 	 		| [[product-list]] 			| 't-shirts'				| Product List 								|
| position 		| [[product-position]] 		| '1'						| Product list position 				 	|

<br />

### Product Click:

- **Where:** The javascript object (dataLayer) below must be fired only once on Click in some product.

```html
<script>
dataLayer.push({
	'event': 'productClick',
	'eventCategory': 'ecommerce',
	'eventAction': 'click_item'
	'ecommerce': {
		'click': {
			'actionField': {'list': '[[product-list]]'},
			'products': [{
				'name': '[[product-name]]',				//Product name or ID is required
				'id': '[[product-id]]',
				'price': '[[product-price]]',
				'brand': '[[product-brand]]',
				'category': '[[product-category]]',
				'variant': '[[product-variant]]',
				'position': '[[product-position]]'
			}]
		}
	}
});
</script>
```

<br />

| Name 			| Variable 					| Exemple 					| Description 							|
| :------------	| :------------------------ | :------------------------ | :-----------------------------------  |
| name 			| [[product-name]] 			| 'compton t-shirt' 		| Product Name 							|
| id			| [[product-id]] 			| '323qe12'					| Product ID							|
| price			| [[product-price]] 		| '44.00' 					| Product Price							|
| brand 		| [[product-brand]] 		| 'compton'					| Product Brand 	 					|
| category 		| [[product-category]] 		| 't-shirt'					| Product Category 						|
| variant 		| [[product-variant]] 		| 'g - amarelo'				| Product Variant (size - color)		|
| list 	 		| [[product-list]] 			| 't-shirts'				| Product List 							|
| position 		| [[product-position]] 		| '1'						| Product List Position 				|

<br />

### Product Detail:

- **Where:** The javascript object (dataLayer) below must be fired once when a product page is loaded.

```html
<script>
dataLayer.push({
	'event': 'productDetail',
	'eventCategory': 'ecommerce',
	'eventAction': 'detail_item'
	'ecommerce': {
		'detail': {
			'actionField': {'list': '[[product-list]]'},
			'products': [{
				'name': '[[product-name]]',				//Product name or ID is required
				'id': '[[product-id]]',
				'price': '[[product-price]]',
				'brand': '[[product-brand]]',
				'category': '[[product-category]]',
				'variant': '[[product-variant]]'
			}]
		}
	}

});
</script>
```

<br />

| Name 			| Variable 					| Exemple 					| Description 								|
| :------------	| :------------------------ | :------------------------ | :---------------------------------------- |
| name 			| [[product-name]] 			| 'compton t-shirt' 		| Product Name 							|
| id			| [[product-id]] 			| '323qe12'					| Product ID							|
| price			| [[product-price]] 		| '44.00' 					| Product Price							|
| brand 		| [[product-brand]] 		| 'compton'					| Product Brand 	 					|
| category 		| [[product-category]] 		| 't-shirt'					| Product Category 						|
| variant 		| [[product-variant]] 		| 'g - amarelo'				| Product Variant (size - color)		|

<br />

### AddToCart:

- **Where:** The javascript object (dataLayer) below must be fired only once in the CTA Click to add a product to the cart.

```html
<script>
dataLayer.push({
	'event': 'addToCart',
	'eventCategory': 'ecommerce',
	'eventAction': 'addToCart'
	'ecommerce': {
		'add': {
			'products': [{
				'name': '[[product-name]]',				//Product name or ID is required
				'id': '[[product-id]]',
				'price': '[[product-price]]',
				'brand': '[[product-brand]]',
				'category': '[[product-category]]',
				'variant': '[[product-variant]]',
				'quantity': '[[quantidade-produto]]'
			}]
		}
	}
});
</script>
```

<br />

| Name 			| Variable 					| Exemple 					| Description 								|
| :------------	| :------------------------ | :------------------------ | :---------------------------------------- |
| name 			| [[product-name]] 			| 'compton t-shirt' 		| Product Name 							|
| id			| [[product-id]] 			| '323qe12'					| Product ID							|
| price			| [[product-price]] 		| '44.00' 					| Product Price							|
| brand 		| [[product-brand]] 		| 'compton'					| Product Brand 	 					|
| category 		| [[product-category]] 		| 't-shirt'					| Product Category 						|
| variant 		| [[product-variant]] 		| 'g - amarelo'				| Product Variant (size - color)		|
| quantity 		| [[quantidade]] 			| '2'						| Quantidade de produtos 				|

<br />

### Remove From Cart:

- **Where:** The javascript object (dataLayer) below must be fired only once in the Click of the button to remove a product from the cart.

```html
<script>
dataLayer.push({
	'event': 'removeFromCart',
	'eventCategory': 'ecommerce',
	'eventAction': 'removeFromCart'
	'ecommerce': {
		'remove': {
			'products': [{
				'name': '[[product-name]]',				//Product name or ID is required
				'id': '[[product-id]]',
				'price': '[[product-price]]',
				'brand': '[[product-brand]]',
				'category': '[[product-category]]',
				'variant': '[[product-variant]]',
				'quantity': '[[quantidade-produto]]'
			}]
		}
	}
});
</script>
```

<br />

| Name 			| Variable 					| Exemple 					| Description 								|
| :------------	| :------------------------ | :------------------------ | :---------------------------------------- |
| name 			| [[product-name]] 			| 'compton t-shirt' 		| Product Name 							|
| id			| [[product-id]] 			| '323qe12'					| Product ID							|
| price			| [[product-price]] 		| '44.00' 					| Product Price							|
| brand 		| [[product-brand]] 		| 'compton'					| Product Brand 	 					|
| category 		| [[product-category]] 		| 't-shirt'					| Product Category 						|
| variant 		| [[product-variant]] 		| 'g - amarelo'				| Product Variant (size - color)		|
| quantity 		| [[quantidade]] 			| '2'						| Quantidade de produtos 				|

<br />

### Promotion Impression:

- **Where:** The javascript object (dataLayer) below must be fired once when viewing a banner.

```html
<script>
dataLayer.push({
	'event': 'promotionImpression',
	'eventCategory': 'ecommerce',
	'eventAction': 'promotion_view'
	'ecommerce': {
		'promoView': {
			'promotions': [{
				'id': '[[id-banner]]',				//Name ou ID do banner é obrigatório
				'name': '[[Name-banner]]',
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

### Conversion Specification:

**Sucess**<br />

- **Where:** Sucess Callback;

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

- **Where:** The javascript object (dataLayer) below must be fired once when the checkout page is loaded.

```html
<script>
dataLayer.push({
	'event': 'checkout',
	'eventCategory': 'ecommerce',
	'eventAction': 'checkout_progress'
	'ecommerce': {
		'checkout': {
			'actionField': {'step': '[[step-checkout]]'},
			'products': [{
				'name': '[[product-name]]',				//Product name or ID is required
				'id': '[[product-id]]',
				'price': '[[product-price]]',
				'brand': '[[product-brand]]',
				'category': '[[product-category]]',
				'variant': '[[product-variant]]',
				'quantity': '[[quantidade-produto]]'
			}]
		}
	}
});
</script>
```

<br />

| Name 			| Variable 					| Exemple 								| Description 						|
| :------------	| :------------------------ | :-----------------------------------  | :----------------------------		|
| actionField 	| [[step-checkout]]			| 'start', 'shipping', 'payment' e etc	| Checkout Step 					|
| name 			| [[product-name]] 			| 'compton t-shirt' 					| Product Name 						|
| id			| [[product-id]] 			| '323qe12'								| Product ID						|
| price			| [[product-price]] 		| '44.00' 								| Product Price						|
| brand 		| [[product-brand]] 		| 'compton'								| Product Brand 	 				|
| category 		| [[product-category]] 		| 't-shirt'								| Product Category 					|
| variant 		| [[product-variant]] 		| 'g - amarelo'							| Product Variant (size - color)	|
| quantity 		| [[quantidade]] 			| '2'									| Quantidade de produtos 			|


<br />

### Purchase:

- **Where:** The javascript object (dataLayer) below must be fired once when the transaction page is loaded, and if the user accesses the link again or refreshes the page, the object must not be fired again.

```html
<script>
dataLayer.push({
	'event': 'purchase',
	'eventCategory': 'ecommerce',
	'eventAction': 'purchase'
	'ecommerce': {
		'purchase': {
			'actionField': {
				'id': '[[transaction-id]]',				//ID da transação é obrigatório
				'affiliation': '[[transaction-affiliate]]',
				'revenue': '[[transaction-revenue]]',
				'tax': '[[transaction-tax]]',
				'shipping': '[[transaction-shipping]]',
				'coupon': '[[transaction-coupon]]'
			},
			'products': [{
				'name': '[[product-name]]',				//Product name or ID is required
				'id': '[[product-id]]',
				'price': '[[product-price]]',
				'brand': '[[product-brand]]',
				'category': '[[product-category]]',
				'variant': '[[product-variant]]',
				'quantity': '[[quantity]]',
				'coupon': '[[cupom-produto]]'
			}]
		}
	}
});
</script>
```

*Purchase Description:*

| Name 			| Variable 					| Exemple 			| Description 										|
| :------------	| :------------------------	| :----------------	| :------------------------------------------------	|
| id 			| [[transaction-id]] 		| '298213890' 		| ID da Transação									|
| affiliation	| [[transaction-affiliate]] | 'xpto' 			| Loja que ocorreu a transação 						|
| revenue 		| [[transaction-revenue]] 	| '85.50' 			| Valor total da transação incluindo frete e taxas	|
| tax 	 		| [[transaction-tax]] 		| '1.00' 			| Taxas da transação 	 							|
| shipping 		| [[transaction-shipping]] 	| '4.50' 			| Frete da transação 								|
| coupon 		| [[transaction-coupon]]	| 'ibbys10off'		| Cupom de desconto usado na transação				|

<br />

*Products Description:*

| Name 			| Variable 					| Exemple 					| Description 						|
| :------------	| :------------------------	| :------------------------ | :--------------------------------	|
| name 			| [[product-name]] 			| 'compton t-shirt' 		| Product Name 						|
| id			| [[product-id]] 			| '323qe12'					| Product ID						|
| price			| [[product-price]] 		| '44.00' 					| Product Price						|
| brand 		| [[product-brand]] 		| 'compton'					| Product Brand 	 				|
| category 		| [[product-category]] 		| 't-shirt'					| Product Category 					|
| variant 		| [[product-variant]] 		| 'g - amarelo'				| Product Variant (size - color)	|
| quantity 		| [[quantity]] 				| '2'						| Quantity 							|
| coupon		| [[cupom-produto]]	 		| 'ibbys10off'				| Cupom de desconto usado no produto|

<br />

<br />

## Final considerations:

> Reference Link: [Official Documentation Google Tag Manager](https://developers.google.com/tag-manager/quickstart)
