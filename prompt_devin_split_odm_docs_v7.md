Você receberá o arquivo `odm_docs_v7_CONSOLIDADO_REVERSIVEL.md`.

Sua tarefa é reconstruir a estrutura original de arquivos a partir dele, sem alterar absolutamente nenhum byte do conteúdo dos arquivos originais.

Regras obrigatórias:

1. O arquivo consolidado usa blocos delimitados por:

   `<!-- ODM_FILE_BEGIN {...} -->`

   e

   `<!-- ODM_FILE_END {...} -->`

2. O JSON dentro de `ODM_FILE_BEGIN` contém, no mínimo:
   - `path`: caminho original do arquivo dentro do ZIP;
   - `bytes`: quantidade exata de bytes UTF-8 do conteúdo original;
   - `sha256`: hash SHA-256 esperado do conteúdo original.

3. Para cada bloco:
   - leia o JSON do `ODM_FILE_BEGIN`;
   - crie o arquivo no caminho indicado por `path`;
   - extraia exatamente os próximos `bytes` bytes UTF-8 após a quebra de linha do marcador `ODM_FILE_BEGIN`;
   - grave esses bytes no arquivo de destino;
   - não normalize quebras de linha;
   - não adicionar newline final;
   - não remover espaços;
   - não reformatar Markdown, CSV ou JSON;
   - não alterar encoding;
   - não reinterpretar o conteúdo.

4. Após gravar cada arquivo:
   - calcule o SHA-256 do conteúdo gravado;
   - compare com o `sha256` declarado no `ODM_FILE_BEGIN`;
   - se qualquer arquivo divergir, interrompa o processo e reporte erro.

5. Ao final, valide:
   - total de arquivos reconstruídos: `361`;
   - total de bytes reconstruídos: `18.444.331`;
   - SHA-256 do arquivo consolidado recebido, se possível:
     `a347e5a8043d7366b9376db0f5911af07900bc8df8fafc68f82c90a40f80a03c`.

6. Depois de reconstruir os arquivos, crie um ZIP com a estrutura reconstruída.

7. Não aplique nenhuma correção, refatoração, melhoria, formatação ou edição no conteúdo. Esta tarefa é apenas split/reconstrução byte-a-byte.

Resultado esperado:
- diretório reconstruído com os 361 arquivos originais;
- relatório informando PASS/FAIL;
- ZIP final reconstruído.
