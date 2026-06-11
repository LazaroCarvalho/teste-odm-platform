# Mensagem para Devin — Reconstrução do ZIP a partir do Markdown Consolidado

Estou enviando o arquivo `plano_implementacao_devin_ai_agent_os_v2_1_CONSOLIDADO_INTEGRO.md`.

Sua tarefa é reconstruir o ZIP original `plano_implementacao_devin_ai_agent_os_v2_1.zip` a partir desse Markdown consolidado, sem alterar, normalizar, reformatar, traduzir ou recriar manualmente nenhum conteúdo.

Use o procedimento descrito no arquivo `PROMPT_DEVIN_RECONSTRUIR_ZIP_A_PARTIR_MD_CONSOLIDADO.md`.

## Regras obrigatórias

1. Use o bloco `ORIGINAL_ZIP_BASE64` como fonte autoritativa para recriar o ZIP original byte-a-byte.

2. Valide o SHA-256 do ZIP reconstruído contra:

```text
1d3aad53a318c0dcdd8e1264055c0cef906fbe6bab61dc5ca03b44da7c601317
```

3. Somente após o hash bater, extraia o ZIP no repositório.

4. Não use os blocos `UTF8_PREVIEW` para reconstrução primária; eles existem apenas para inspeção humana.

5. Se qualquer hash ou contagem divergir, pare e reporte:

```text
NO_GO_INTEGRITY_FAILURE
```

6. Não implemente nada ainda. Apenas reconstrua, valide e reporte o resultado.

## Resultado esperado

```text
PASS_RECONSTRUCTION_INTEGRITY_VERIFIED
```
