# Relatório — Laboratório de Inspeção HTTP/HTTPS — Fluxo A (Administrador)

> **Como usar este template.** Preencha cada campo `[...]` com sua resposta e arraste as capturas de tela diretamente para os locais indicados. Preserve a formatação Markdown.
>
> **Escopo:** este fluxo inclui HTTP em texto claro, HTTPS sem decriptação e HTTPS com decriptação TLS pelo Fiddler Classic.

---

## Como anexar capturas de tela

1. Faça a captura de tela e salve como PNG.
2. No editor do GitHub ou GitHub.dev, posicione o cursor no local indicado.
3. Arraste o PNG para o editor. O GitHub inserirá uma linha `![image](...)`.

---

## Identificação

| Campo | Valor |
|---|---|
| Nome | Julliano Angelotti Giacomini - Laryssa Flabio Ignacio |
| RA | 242960 - 240274 |
| Disciplina | Redes de Computadores |
| Turma | Turma A - Noite |
| Data | 15/05 |
| Fluxo | **A — Aluno com privilégio de administrador** |
| SO utilizado | Windows 10 |
| Ferramenta de proxy | Fiddler Classic |
| Navegador(es) | Chrome ] |
| Decriptação HTTPS habilitada? | sim |
| Certificado Fiddler instalado durante a atividade? | sim |

---

## Atividade 1 — Primeira captura

### Captura
<img width="955" height="936" alt="Captura1" src="https://github.com/user-attachments/assets/7d833e0f-b811-4d4a-9004-a94d125cc8e5" />

**Request-line:**

GET https://httpbingo.org/get HTTP/1.1

**Status-line:**

HTTP/1.1 200 OK

**Cabeçalhos do request:**

| Cabeçalho | Função |
|---|---|
| access-control-allow-credentials: true | Permite envio de cookies/auth em CORS |
| access-control-allow-origin: * | Libera acesso para qualquer origem |
| content-encoding: zstd | Resposta comprimida com Zstandard |

**Resposta:**

| Campo | Valor observado |
|---|---|
| Content-Type | application/json; charset=utf-8 |
| transfer-encoding | chunked |

---

## Atividade 2 — Anatomia de um GET


### Captura
<img width="957" height="1052" alt="Captura2" src="https://github.com/user-attachments/assets/d7d64c04-7c37-4361-b927-1315ff566897" />

**Request-line completa:**

GET https://httpbingo.org/get?aluno=SEU_NOME&curso=redes HTTP/1.1

**Cabeçalhos-chave:**

| Cabeçalho | Valor |
|---|---|
| Host | httpbingo.org |
| User-Agent | Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36 |
| Accept | text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7 |

**Campos do JSON de resposta:**

```json
{
  "args": [colar valor],
  "headers": [colar valor resumido],
  "origin": [colar valor]
}
```

**Resposta curta:** o que o campo `origin` representa? O `User-Agent` retornado coincide com o enviado?

Origin representa a origem do navegador e o user-agent representa o agente de texto do navegador


---

## Atividade 3 — POST e envio de formulário

### Captura
<img width="952" height="1031" alt="Captura3" src="https://github.com/user-attachments/assets/43e3c464-356f-46fb-8f9c-94d80ae46302" />

**Request-line do POST:**

POST https://httpbingo.org/post HTTP/1.1

| Cabeçalho | Valor |
|---|---|
| Content-Type | application/x-www-form-urlencoded |
| Content-Length | 129 |

**Corpo do request:**

custname=Julliano+&custtel=13974218808&custemail=julliano.ag%40gmail.com&size=small&topping=bacon&delivery=12%3A45&comments=teste

**Campo `form` da resposta:**


**Resposta curta:** qual formato codifica o corpo? Qual aba mostra literalmente os bytes enviados: `WebForms` ou `Raw`?

Ele utiliza x-www-form-urlencoded, mostrado na raw

---

## Atividade 4 — Status codes

### Captura

<!-- arraste a captura aqui: lista do Fiddler com as quatro sessões -->

| # | Método | URL | Status-line | Tamanho/body |
|---|---|---|---|---|
| 1 | POST | https://httpbingo.org/status/200 | 200 | Sem body |
| 2 | GET | https://httpbingo.org/redirect-to?status_code=301&url=/get | 301 | sem body |
| 3 | GET | https://httpbingo.org/status/404 | 404 | Sem body |
| 4 | GET | https://httpbingo.org/status/500 | 500 | Sem body |

**Resposta curta:** no `301`, qual cabeçalho informa o destino do redirecionamento?


Location: /get

---

## Atividade 5 — Cabeçalhos essenciais

### Captura
<img width="955" height="1027" alt="Captura4" src="https://github.com/user-attachments/assets/795c18fd-374f-43d7-8421-aafdd68408f2" />


| Cabeçalho | Req/Resp | Valor capturado | Função |
|---|---|---|---|
| `Host` | Req | `http.aulasrede.com.br` | Indica o servidor de destino da requisição |
| `User-Agent` | Req | `Mozilla/5.0 (...) Chrome/142.0.0.0 Safari/537.36` | Identifica navegador e sistema operacional do cliente |
| `Accept` | Req | `text/html,application/xhtml+xml,...` | Informa os tipos de conteúdo aceitos pelo cliente |
| `Content-Type` | Resp | `text/html; charset=utf-8` | Define o tipo de conteúdo retornado |
| `Content-Length` / `Transfer-Encoding` | Resp | `Content-Length: ...` ou `Transfer-Encoding: chunked` | Define tamanho do corpo ou envio em partes |
| `Content-Encoding` | Resp | `gzip`, `br` ou `zstd` | Indica compressão aplicada ao corpo |
| `Set-Cookie` | Resp | `teste=1` | Cria/define cookie no navegador |
| `Cache-Control` | Resp | `max-age=3600` | Define política de cache da resposta |
| `Strict-Transport-Security` | Resp | `max-age=31536000` | Obriga uso de HTTPS por 1 ano |

**Resposta curta:** qual é o papel de `Content-Encoding` e de `Strict-Transport-Security`?
Definir o formato de criptografia do conteudo, e o strict serve para obrigar o site a usar https

---

## Atividade 6 — HTTP vs HTTPS

### Captura — HTTP puro
<img width="947" height="995" alt="Captura5" src="https://github.com/user-attachments/assets/af576aa3-77fc-414b-873b-28f3b0a957dd" />


### Captura — HTTPS sem decriptação
<img width="957" height="1052" alt="Captura6" src="https://github.com/user-attachments/assets/a05935af-e1ea-44f5-b478-3b0e045a39fe" />


### Captura — HTTPS com decriptação
<img width="952" height="1037" alt="Captura7" src="https://github.com/user-attachments/assets/125f019f-7ca4-4a8d-bde5-786e17fb5450" />


| Situação | O que ficou visível? | O que ficou oculto? |
|---|---|---|
| HTTP puro | request | response|
| HTTPS sem decriptação | request | response |
| HTTPS com decriptação | request e response| |

**Resposta curta:** por que a decriptação HTTPS pelo Fiddler exige instalar um certificado raiz?
Pois é a partir do certificado que é feita a validação e decriptação do conteudo do http

[resposta]

---

## Atividade 7 — Cookies e sessão

### Captura
<img width="959" height="1053" alt="Captura8" src="https://github.com/user-attachments/assets/760efcc1-f1cf-4ce7-a8a6-5de0cc8d1fcd" />


| # | URL | `Set-Cookie` recebido | `Cookie` enviado |
|---|---|---|---|
| 1 | /cookies/set?... | disciplina=redes, professor=claudio | — |
| 2 | /cookies | — | disciplina=redes; professor=claudio |
| 3 | /cookies após recarregar | — | disciplina=redes; professor=claudio |

**Resposta curta:** `Set-Cookie` apareceu em toda requisição ou apenas quando o servidor definiu/atualizou cookies? Quais atributos foram observados?

Set-Cookie apareceu apenas quando o servidor definiu/atualizou cookies. Os atributos observados incluíram nome/valor do cookie e, em alguns casos, Path, Expires, Max-Age, HttpOnly, Secure e SameSite.

---

## Atividade 8 — Manipulação simples com breakpoint *(Opcional)*

### Captura

<!-- arraste a captura aqui: breakpoint com User-Agent editado -->

**JSON de resposta:**

```json
{
  "user-agent": ["[valor observado]"]
}
```

**Resposta curta:** o que este teste mostra sobre o papel ativo de um proxy?

[resposta]

- [ ] Breakpoints desabilitados ao final

---

## Reflexão final (opcional)

[até 10 linhas]

---

## Encerramento — Higiene de segurança

### Captura antes da remoção

<!-- arraste aqui a captura do certmgr.msc mostrando DO_NOT_TRUST_FiddlerRoot presente -->

### Captura depois da remoção

<!-- arraste aqui a captura mostrando o certificado ausente -->

- [ ] `Decrypt HTTPS traffic` desabilitado no Fiddler
- [ ] Certificado `DO_NOT_TRUST_FiddlerRoot` removido do Windows
- [ ] Certificado `DO_NOT_TRUST_FiddlerRoot` removido do Firefox, se aplicável
- [ ] Fiddler fechado

**Por que esta etapa é importante?**

[resposta curta]

---

## Checklist de entrega

- [ ] Campos `[...]` substituídos
- [ ] Capturas inseridas
- [ ] Atividades 1 a 7 preenchidas; Atividade 8 preenchida se executada
- [ ] Encerramento com duas capturas concluído
- [ ] PDF gerado como `SOBRENOME_NOME_RA_LAB_HTTP_FLUXOA.pdf`
- [ ] PDF submetido no Microsoft Teams
