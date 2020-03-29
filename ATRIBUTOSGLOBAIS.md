## Atributos Globais

**atributos de um elemento HTML** = Fornecem informações adicionais sobre o elemento. Sempre definidos na tag de abertura. Geralmente são do tipo *nome="valor"*, mas também podem ser somente *nome* caso o valor seja igual ao nome do atributo.

Todos os elementos HTML possuem ou podem possuir atributos. Só que existem atributos que são comuns a todos os elementos HTML, os chamados **atributos globais**

- accesskey -> define uma tecla de atalho para focar na tag
- class -> define uma classe CSS. Podemos definir uma classe para mais de um elemento.
- contenteditable -> quando não usamos input, mas queremos que a tag seja editável. Por padrão é **false**
- data-* -> usado para armazenar dados em um elemento. No lugar do * usamos qualquer nome
- dir -> especifica a direção de leitura de um elemento. ex.: da direita para a esquerda
- draggable -> define se um elemento pode ou não ser arrastado. Por padrão é **false**
- dropzone -> define o local onde um elemento arrastado pode ser colocado
- hidden -> define o elemento como oculto
- id -> define uma identificação única de um elemento. Usado para CSS e Javascript
- lang -> define a linguagem/idioma
- spellcheck -> define se no elemento deve ser verificado a ortografia. Por padrão é **false**
- style -> define estilos CSS diretamente no elemento
- tabindex -> define a ordem de tabulação do elemento na pagina. Foco da tecla TAB
- title -> define informações sobre o elemento, pra que que ele serve ou para onde o link é direcionado. Aparece como um tooltip quando passamos o mouse em cima
- translate -> define se o elemento pode ser traduzido ou não

## accesskey

No chrome/Edge usamos a tela ALT + a tecla de atalho definida no atributo.
No firefox ALT + SHIFT + a tecla de atalho definida no atributo.

Como vimos para cada navegardor temos uma forma de executar. Para deixar a tecla de atalho comum a todos, necessitamos usar Javascript para isso.

```html
<button type="button" accesskey="n">Novo</button>
```

## contenteditable

Ele recebe um *true* ou *false* como valor. Por padrão, se não for atribuido nenhum valor é tratado como **false**. Ele só edita em tempo de execução, ou seja, ao atualizar a pagina volta ao conteudo original. Podemos usar JS para salvar a edição.

## data

atributo onde guardamos informações pertinentes que poderão ser utilizadas em algum lugar.

```html
<ul>
    <li data-id="1" data-email="figueiredoaphilippe@gmail.com">André Figueiredo</li>
    <li data-id="2" data-email="glaucio@hcode.com.br">Glaudio Daniel</li>
</ul>

<script>
    document.querySelectorAll('li').forEach(element => {
        console.log(element.dataset);
    })
</script>
```

## dir (direction)

Usado quando o site é visitado não somente no pais de origem.

Temos os valores:

- auto -> quando respeita o padrão do sistema operacional de origem
- ltr -> quando é lido da esquerda para a direita
- rtl -> quando é lido da direita para a esquerda

## drozone

Local onde o conteudo arrastável é posicionado.

- copy -> soltar os dados resultará em uma cópia dos dados arrastados
- move -> soltar os dados fará com que os dados arrastados sejam movidos para o novo local
- link -> soltar os dados resultará em um link para os dados originais

Ainda não está 100% funcional para os navegadores. Hoje em dia é necessário usar JS para aplicar essas ações.

```html
<script>
    const caixa = document.querySelectorAll('.caixa');
    const dropzone = document.querySelector('[dropzone]');

    caixa.forEach(caixaEl => {  
        // adiciona aos elementos um listener no evento de dragstart
        caixaEl.addEventListener('dragstart', e => {
            e.dataTransfer.setData('Text', e.target.id); // seta o dipo de dado da transferencia
            console.log('arrastando -> ', e.target.id)
        })
    });

    // cancela o evento padrão dos navegadores de soltar um draggable
    dropzone.addEventListener('dragover', e => { e.preventDefault(); });

    // ao soltar o draggable no elemento com atributo dropzone
    dropzone.addEventListener('drop', e => {
        console.log('soltando -> ', e.dataTransfer.getData('Text'));
        const id = e.dataTransfer.getData('Text');
        const element = document.getElementById(id);
        e.target.appendChild(element);
    })
</script>
```

## hidden (escondido)

```html
<div hidden>Esta div está escondida para o usuario</div>
```

## lang (language)

Geralmente é um atributo usado para tradutores e motores de busca ou leitores de pagina que usarão a pronuncia correta para a tag que tiver esse atributo.

## spellcheck (verificação ortográfica)

É usada quando o conteúdo é editado pelo usuario. Geralmente em conjunto com o atributo contenteditable.

## tabIndex (tabulação)

Define a ordem de tabulação da página. Quando apertamos a tecla tab ele segue a ordem do tabIndex.

```html
<input type="text" name="email" placeholder="email" tabindex="1">
<input type="text" name="senha" placeholder="senha" tabindex="2">
<button type="button" tabindex="4">limpar</button>
<button type="button" tabindex="3">enviar</button>
```

## title 

Usado para dar informação do que uma determinada tag faz ou significa. Muito usado em motores de busca, leitores de paginas onde ajuda muito a entender o que aquele elemento se propoe a fazer para quem está ouvindo.

## translate

```html
<elemento translate="yes|no">
```