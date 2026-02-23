# Configuração de Lifecycle no Amazon S3
Este exemplo demonstra como configurar uma regra de **Lifecycle** no bucket `foo-bucket` para mover objetos automaticamente para a classe **GLACIER** após 180 dias.
---
Mover automaticamente todos os objetos do bucket para a classe de armazenamento **GLACIER** após 6 meses (180 dias), reduzindo custos de armazenamento.
---
##1. Criar o arquivo de configuração
Crie um arquivo chamado `lifecycle.json` com o seguinte conteúdo:
```json
{
  "Rules": [
    {
      "ID": "MoveToGlacierAfter180Days",
      "Filter": {
        "Prefix": ""
      },
      "Status": "Enabled",
      "Transitions": [
        {
          "Days": 180,
          "StorageClass": "GLACIER"
        }
      ]
    }
  ]
}
````
##2. Aplicar a regra ao bucket
Execute o comando abaixo para aplicar a configuração:

````bash
aws s3api put-bucket-lifecycle-configuration \
  --bucket foo-bucket \
  --lifecycle-configuration file://lifecycle.json
````
