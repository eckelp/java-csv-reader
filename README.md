# java-csv-reader

## Read CSV with jackson

### MAVEN


```
 <dependency>
    <groupId>com.fasterxml.jackson.dataformat</groupId>
    <artifactId>jackson-dataformat-csv</artifactId>
    <version>2.11.1</version>
</dependency>

<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.11.1</version>
</dependency>
```

### Leitura de arquivo

Neste exemplo o arquivo deve estar na pasta `resources` 
Mas é possível refatorar o método para receber o `File` convertido do `Multipartfile` da request. [Link aqui](https://www.baeldung.com/spring-multipartfile-to-file)

```
private final String PATH_ARQUIVO = "nome_do_arquivo.csv";
private final char SEPARADOR = ';';

public List<AlgumDtoQualquer> lerArquivoUrls() {

    try {
        CsvSchema urlsSchema = CsvSchema
            .emptySchema()
            .withHeader()
            .withColumnSeparator(SEPARADOR);

        File file = getFile(PATH_ARQUIVO);

        MappingIterator<UrlDto> linhas = csvMapper
            .readerFor(AlgumDtoQualquer.class)
            .with(urlsSchema)
            .readValues(file);

        return linhas.readAll();

    } catch (Exception e) {
        e.printStackTrace();
        throw new RuntimeException("Não foi possível ler o arquivo");
    }
}
```
