link do lab: [https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-string-angle-brackets-html-encoded](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-string-angle-brackets-html-encoded)

# **Lab: Reflected XSS into a JavaScript string with angle brackets HTML encoded**

O principal Objetivo do Lab é executar a função JS `alert()` via XSS refletido.

<img width="567" height="324" alt="image" src="https://github.com/user-attachments/assets/e1a2ecc8-0d58-47ec-a2c6-0737cacfb5fc" />

---

## 1. Análise da Vulnerabilidade e Contexto de Injeção

Ao injetar um termo simples (ex.: `oi`) no campo de busca, observei que o valor era refletido na página dentro de uma variável JavaScript. O contexto de injeção era o seguinte:

<img width="567" height="127" alt="image" src="https://github.com/user-attachments/assets/dc2ab491-7b4d-4144-a4b8-37208988e1f3" />

Após analisar o código, percebi que meu input era refletido dentro de uma string JavaScript delimitada por aspas simples. Então tive a ideia de injetar `oi'; alert(); //` para ver o comportamento.

<img width="567" height="174" alt="image" src="https://github.com/user-attachments/assets/420020d6-e9b4-46aa-9f7a-3efba683b530" />

O código por inteiro virou uma string:

<img width="567" height="127" alt="image" src="https://github.com/user-attachments/assets/9dc924b7-61ef-4db4-8852-458f0d443d1e" />

---

### Como o payload funciona

A chave foi **quebrar a string original**. Eu fechei a string com a aspa simples (`'`) logo depois do `oi`. Isso permitiu que o `alert()` fosse lido como um comando JavaScript válido logo em seguida. Finalizei com `//`, que é o comentário de linha única no JavaScript, garantindo que o restante do código da linha fosse ignorado e que o ataque não causasse um erro de sintaxe.

Exemplo do input que usei:

```
oi'; alert(); //
```

Resultado refletido na página (exemplo):

```javascript
var searchTerms = 'oi'; alert(); //';
```

Com isso, `alert()` é executado e o lab é solucionado.

---

## 2. Payload / Prova de Conceito (PoC)

Use o payload abaixo no campo de busca do lab para disparar o `alert()`:

```
';alert(1);//
```

Esse payload fecha a string, executa `alert(1)` e comenta o resto da linha.

---

## 3. Mitigações e Recomendações

* **Escapar/serializar** os valores inseridos dentro de strings JavaScript (usar `JSON.stringify()` ao inserir valores em `<script>` é uma boa prática).
* Evitar interpolar diretamente dados do usuário em blocos `<script>`; prefira atribuir dados via `data-attributes` ou *text nodes* e ler com `textContent`/`dataset`.
* Aplicar validação de entrada e codificação de saída conforme o contexto (HTML, atributo, JS, URL).

---

## 4. Observações finais

* Use esse PoC apenas em ambientes de teste autorizados (ex.: PortSwigger Web Security Academy).
* As imagens presentes no documento ilustram os passos realizados durante a exploração.

---

> **Créditos:** Conteúdo criado para fins educativos e documentação de aprendizado.
