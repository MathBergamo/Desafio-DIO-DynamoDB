### Funcionalidades adicionadas:

:sparkles: PESQUISR ITEM PELO ANO

aws dynamodb query \
    --table-name Music \
    --key-condition-expression "SongYear = :v_year" \
    --expression-attribute-values  '{":v_year":{"S":"2001"}}'


:sparkles: CRIAR UM INDEX GLOBAL BASEADO NO NOME DA BANDA E NO ANO

aws dynamodb update-table \
    --table-name Music \
    --attribute-definitions\
        AttributeName=Artist,AttributeType=S \
        AttributeName=SongYear,AttributeType=S \
    --global-secondary-index-updates \
        "[{\"Create\":{\"IndexName\": \"ArtistYear-index\",\"KeySchema\":[{\"AttributeName\":\"Artist\",\"KeyType\":\"HASH\"}, {\"AttributeName\":\"SongYear\",\"KeyType\":\"RANGE\"}], \
        \"ProvisionedThroughput\": {\"ReadCapacityUnits\": 10, \"WriteCapacityUnits\": 5      },\"Projection\":{\"ProjectionType\":\"ALL\"}}}]"


