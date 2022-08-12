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


**1 - Quero Veloe - Menu:**<br />

- **Quando:** Ao clicar no botao do menu;
- **Onde:** Menu principal;

```html
dataLayer.push({
		'event': 'event',
		'nome-evento': 'quero veloe - menu'
	});
```

<br />


**2 - Quero Veloe - Banner:**<br />

- **Quando:** Ao clicar no botao do banner;
- **Onde:** Menu principal;

```html
dataLayer.push({
		'event': 'event',
		'nome-evento': 'quero veloe - banner'
	});
```

<br />


**3 - Quero Veloe - Planos:**<br />

- **Quando:** Ao clicar no botao abaixo do compartivo dos Planos;
- **Onde:** Comparativo de Planos;

```html
dataLayer.push({
		'event': 'event',
		'nome-evento': 'quero veloe - planos'
	});
```


---

<br />

## Considerações Finais:

> Link de referência: [Documentação Oficial Google Tag Manager](https://developers.google.com/tag-manager/quickstart)
