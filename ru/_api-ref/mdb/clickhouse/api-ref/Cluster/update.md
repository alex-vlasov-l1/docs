---
editable: false
---

# Метод update
Изменяет указанный кластер ClickHouse.
 

 
## HTTP-запрос {#https-request}
```
PATCH https://mdb.api.cloud.yandex.net/managed-clickhouse/v1/clusters/{clusterId}
```
 
## Path-параметры {#path_params}
 
Параметр | Описание
--- | ---
clusterId | Обязательное поле. Идентификатор ресурса Cluster для ClickHouse, который следует обновить. Чтобы получить идентификатор кластера ClickHouse, используйте запрос [list](/docs/managed-clickhouse/api-ref/Cluster/list).  Максимальная длина строки в символах — 50.
 
## Параметры в теле запроса {#body_params}
 
```json 
{
  "updateMask": "string",
  "description": "string",
  "labels": "object",
  "configSpec": {
    "version": "string",
    "clickhouse": {
      "config": {
        "logLevel": "string",
        "mergeTree": {
          "replicatedDeduplicationWindow": "integer",
          "replicatedDeduplicationWindowSeconds": "integer"
        },
        "compression": [
          {
            "method": "string",
            "minPartSize": "string",
            "minPartSizeRatio": "number"
          }
        ],
        "dictionaries": [
          {
            "name": "string",
            "structure": {
              "id": {
                "name": "string"
              },
              "key": {
                "attributes": [
                  {
                    "name": "string",
                    "type": "string",
                    "nullValue": "string",
                    "expression": "string",
                    "hierarchical": true,
                    "injective": true
                  }
                ]
              },
              "attributes": [
                {
                  "name": "string",
                  "type": "string",
                  "nullValue": "string",
                  "expression": "string",
                  "hierarchical": true,
                  "injective": true
                }
              ]
            },
            "layout": {
              "type": "string",
              "sizeInCells": "string"
            },

            // `configSpec.clickhouse.config.dictionaries[]` включает только одно из полей `httpSource`, `mysqlSource`, `clickhouseSource`, `mongodbSource`
            "fixedLifetime": "string",
            "lifetimeRange": {
              "min": "string",
              "max": "string"
            },
            // конец списка возможных полей`configSpec.clickhouse.config.dictionaries[]`

            "httpSource": {
              "url": "string",
              "format": "string"
            },
            "mysqlSource": {
              "db": "string",
              "table": "string",
              "port": "string",
              "user": "string",
              "password": "string",
              "replicas": [
                {
                  "host": "string",
                  "priority": "string",
                  "port": "string",
                  "user": "string",
                  "password": "string"
                }
              ],
              "where": "string",
              "invalidateQuery": "string"
            },
            "clickhouseSource": {
              "db": "string",
              "table": "string",
              "host": "string",
              "port": "string",
              "user": "string",
              "password": "string",
              "where": "string"
            },
            "mongodbSource": {
              "db": "string",
              "collection": "string",
              "host": "string",
              "port": "string",
              "user": "string",
              "password": "string"
            }
          }
        ],
        "graphiteRollup": [
          {
            "name": "string",
            "patterns": [
              {
                "regexp": "string",
                "function": "string",
                "retention": [
                  {
                    "age": "string",
                    "precision": "string"
                  }
                ]
              }
            ]
          }
        ],
        "maxConnections": "integer",
        "maxConcurrentQueries": "integer",
        "keepAliveTimeout": "integer",
        "uncompressedCacheSize": "integer",
        "markCacheSize": "integer",
        "maxTableSizeToDrop": "integer",
        "maxPartitionSizeToDrop": "integer",
        "builtinDictionariesReloadInterval": "integer",
        "timezone": "string"
      },
      "resources": {
        "resourcePresetId": "string",
        "diskSize": "string",
        "diskTypeId": "string"
      }
    },
    "zookeeper": {
      "resources": {
        "resourcePresetId": "string",
        "diskSize": "string",
        "diskTypeId": "string"
      }
    },
    "backupWindowStart": {
      "hours": "integer",
      "minutes": "integer",
      "seconds": "integer",
      "nanos": "integer"
    }
  }
}
```

 
Поле | Описание
--- | ---
updateMask | **string**<br><p>Маска, которая указывает, какие поля ресурса Cluster для ClickHouse должны быть изменены.</p> <p>Имена всех обновляемых полей, разделенные запятыми. Только значения указанных полей будут изменены. Остальные останутся нетронутыми. Если поле указано в параметре <code>updateMask</code> и в запросе не было отправлено значение для этого поля, значение поля будет сброшено на значение по умолчанию. Значение по умолчанию для большинства полей — null или 0.</p> <p>Если в запросе не передается <code>updateMask</code>, значения всех полей будут обновлены. Для полей, указанных в запросе, будут использованы переданные значения. Значения остальных полей будут сброшены на значения по умолчанию.</p> 
description | **string**<br><p>Новое описание кластера ClickHouse.</p> <p>Максимальная длина строки в символах — 256.</p> 
labels | **object**<br><p>Пользовательские метки для кластера ClickHouse как пары <code>key:value</code>. Максимум 64 на ресурс. Например, &quot;project&quot;: &quot;mvp&quot; или &quot;source&quot;: &quot;dictionary&quot;.</p> <p>Новый набор меток полностью заменит старый. Чтобы добавить метку, запросите текущий набор меток с помощью метода <a href="/docs/managed-clickhouse/api-ref/Cluster/get">get</a>, затем отправьте запрос <a href="/docs/managed-clickhouse/api-ref/Cluster/update">update</a>, добавив новую метку в этот набор.</p> <p>Не более 64 на ресурс. Максимальная длина строки в символах для каждого ключа — 63. Каждый ключ должен соответствовать регулярному выражению <code>[a-z][-_0-9a-z]*</code>. Максимальная длина строки в символах для каждого значения — 63. Каждое значение должно соответствовать регулярному выражению <code>[-_0-9a-z]*</code>.</p> 
configSpec | **object**<br><p>Новая конфигурация и ресурсы для хостов кластера.</p> 
configSpec.<br>version | **string**<br><p>Версия серверного программного обеспечения ClickHouse.</p> 
configSpec.<br>clickhouse | **object**<br><p>Конфигурация и ресурсы для сервера ClickHouse.</p> 
configSpec.<br>clickhouse.<br>config | **object**<br><p>Конфигурация для сервера ClickHouse.</p> <p>Настройки конфигурации ClickHouse. Подробное описание для каждого набора настроек доступно в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/">документации ClickHouse</a>.</p> <p>Любые настройки, не перечисленные здесь, не поддерживаются.</p> 
configSpec.<br>clickhouse.<br>config.<br>logLevel | **string**<br><p>Уровень логирования для кластера ClickHouse.</p> 
configSpec.<br>clickhouse.<br>config.<br>mergeTree | **object**<br><p>Параметры движка MergeTree. См. описание в <a href="https://clickhouse.yandex/docs/en/operations/server_settings/settings/#merge_tree">документации ClickHouse</a>.</p> <p>Настройки движка таблицы MergeTree.</p> 
configSpec.<br>clickhouse.<br>config.<br>mergeTree.<br>replicatedDeduplicationWindow | **integer** (int64)<br><p>Количество блоков хэшей, которые должен хранить ZooKeeper. Смотрите подробное описание в <a href="https://github.com/yandex/ClickHouse/blob/v18.1.0-stable/dbms/src/Storages/MergeTree/MergeTreeSettings.h#L59">исходном коде ClickHouse</a>.</p> 
configSpec.<br>clickhouse.<br>config.<br>mergeTree.<br>replicatedDeduplicationWindowSeconds | **integer** (int64)<br><p>Период времени, в течение которого следует хранить блоки хэшей. См. описание в <a href="https://github.com/yandex/ClickHouse/blob/v18.1.0-stable/dbms/src/Storages/MergeTree/MergeTreeSettings.h#L64">исходном коде ClickHouse</a>.</p> 
configSpec.<br>clickhouse.<br>config.<br>compression[] | **object**<br><p>Параметры сжатия для кластера ClickHouse. См. подробное описание в <a href="https://clickhouse.yandex/docs/en/operations/server_settings/settings/#compression">документации ClickHouse</a>.</p> 
configSpec.<br>clickhouse.<br>config.<br>compression[].<br>method | **string**<br><p>Метод сжатия, используемый для указанной комбинации <code>min_part_size</code> и <code>min_part_size_ratio</code>.</p> <ul> <li>LZ4: <a href="https://lz4.github.io/lz4/">Алгоритм сжатия LZ4</a>.</li> <li>ZSTD: <a href="https://facebook.github.io/zstd/">Алгоритм сжатия Zstandard</a>.</li> </ul> 
configSpec.<br>clickhouse.<br>config.<br>compression[].<br>minPartSize | **string** (int64)<br><p>Минимальный размер части таблицы.</p> <p>Минимальное значение — 1.</p> 
configSpec.<br>clickhouse.<br>config.<br>compression[].<br>minPartSizeRatio | **number** (double)<br><p>Минимальное отношение части к размеру всех данных в таблице.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[] | **object**<br><p>Конфигурация внешних словарей для кластера ClickHouse. См. подробное описание в <a href="https://clickhouse.yandex/docs/en/query_language/dicts/external_dicts/">документации ClickHouse</a>.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>name | **string**<br><p>Обязательное поле. Имя внешнего словаря.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>structure | **object**<br>Обязательное поле. Набор атрибутов внешнего словаря. Подробное описание см. в [документации ClickHouse](https://clickhouse.yandex/docs/en/query_language/dicts/external_dicts_dict_structure/).<br>
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>structure.<br>id | **object**<br><p>Один столбец с числовыми ключами для словаря.</p> <p>Числовой ключ.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>structure.<br>id.<br>name | **string**<br><p>Обязательное поле. Имя числового ключа.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>structure.<br>key | **object**<br><p>Составной ключ для словаря, содержащего один или несколько столбцов с ключами. Подробнее см. в <a href="https://clickhouse.yandex/docs/en/query_language/dicts/external_dicts_dict_structure/#composite-key">документации ClickHouse</a>.</p> <p>Составной ключ.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>structure.<br>key.<br>attributes[] | **object**<br><p>Обязательное поле. Поля составного ключа.</p> <p>Должен содержать хотя бы один элемент.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>structure.<br>key.<br>attributes[].<br>name | **string**<br><p>Обязательное поле. Имя столбца.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>structure.<br>key.<br>attributes[].<br>type | **string**<br><p>Обязательное поле. Тип столбца.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>structure.<br>key.<br>attributes[].<br>nullValue | **string**<br><p>Значение по умолчанию для элемента без данных (например, пустая строка).</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>structure.<br>key.<br>attributes[].<br>expression | **string**<br><p>Выражение, описывающее атрибут, если применимо.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>structure.<br>key.<br>attributes[].<br>hierarchical | **boolean** (boolean)<br><p>Признак поддержки иерархии. Значение по умолчанию: &quot;false&quot;.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>structure.<br>key.<br>attributes[].<br>injective | **boolean** (boolean)<br><p>Признакт инъективного отображения &quot;id -&gt; атрибут&quot;. Значение по умолчанию: &quot;false&quot;.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>structure.<br>attributes[] | **object**<br><p>Обязательное поле. Описание полей, доступных для запросов к базе данных. Подробнее см. в <a href="https://clickhouse.yandex/docs/en/query_language/dicts/external_dicts_dict_structure/#attributes">документации ClickHouse</a>.</p> <p>Должен содержать хотя бы один элемент.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>structure.<br>attributes[].<br>name | **string**<br><p>Обязательное поле. Имя столбца.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>structure.<br>attributes[].<br>type | **string**<br><p>Обязательное поле. Тип столбца.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>structure.<br>attributes[].<br>nullValue | **string**<br><p>Значение по умолчанию для элемента без данных (например, пустая строка).</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>structure.<br>attributes[].<br>expression | **string**<br><p>Выражение, описывающее атрибут, если применимо.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>structure.<br>attributes[].<br>hierarchical | **boolean** (boolean)<br><p>Признак поддержки иерархии. Значение по умолчанию: &quot;false&quot;.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>structure.<br>attributes[].<br>injective | **boolean** (boolean)<br><p>Признакт инъективного отображения &quot;id -&gt; атрибут&quot;. Значение по умолчанию: &quot;false&quot;.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>layout | **object**<br>Обязательное поле. Макет для хранения словаря в памяти. Подробное описание см. в [документации ClickHouse](https://clickhouse.yandex/docs/en/query_language/dicts/external_dicts_dict_layout/).<br><p>Макет, определяющий способ хранения словаря в памяти.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>layout.<br>type | **string**<br><p>Обязательное поле. Тип макета для внешнего словаря.</p> <ul> <li>FLAT: Весь словарь хранится в памяти в виде плоских массивов. Доступно для любых источников словарей.</li> <li>HASHED: Весь словарь хранится в памяти в виде хэш-таблицы. Доступно для любых источников словарей.</li> <li>COMPLEX_KEY_HASHED: Аналогичен HASHED, для использования с составными ключами. Доступно для любых источников словарей.</li> <li>RANGE_HASHED: Весь словарь хранится в памяти в виде хэш-таблицы, с упорядоченным массивом диапазонов и соответствующих им значений. Доступно для любых источников словарей.</li> <li>CACHE: Словарь хранится в кэше с заданным количеством ячеек. Доступно для источников словарей MySQL, ClickHouse и HTTP.</li> <li>COMPLEX_KEY_CACHE: Аналогичен CACHE, для использования с составными ключами. Доступно для источников словарей MySQL, ClickHouse и HTTP.</li> </ul> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>layout.<br>sizeInCells | **string** (int64)<br><p>Количество ячеек в кэше. Округляется до степени двойки. Применимо только для типов макета CACHE и COMPLEX_KEY_CACHE.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>fixedLifetime | **string** (int64) <br>`configSpec.clickhouse.config.dictionaries[]` включает только одно из полей `fixedLifetime`, `lifetimeRange`<br><br><p>Жесткий интервал между обновлениями словаря.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>lifetimeRange | **object**<br>Диапазон интервалов между обновлениями словаря, из которых может выбирать ClickHouse. <br>`configSpec.clickhouse.config.dictionaries[]` включает только одно из полей `fixedLifetime`, `lifetimeRange`<br><br>
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>lifetimeRange.<br>min | **string** (int64)<br><p>Минимальное время жизни словаря.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>lifetimeRange.<br>max | **string** (int64)<br><p>Максимальное время жизни словаря.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>httpSource | **object**<br>HTTP-источник для словаря. <br>`configSpec.clickhouse.config.dictionaries[]` включает только одно из полей `httpSource`, `mysqlSource`, `clickhouseSource`, `mongodbSource`<br><br>
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>httpSource.<br>url | **string**<br><p>Обязательное поле. URL внешнего словаря, доступного по HTTP.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>httpSource.<br>format | **string**<br><p>Обязательное поле. Формат данных. Допустимые значения: все форматы, поддерживаемые диалектом ClickHouse SQL.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>mysqlSource | **object**<br>MySQL-источник для словаря. <br>`configSpec.clickhouse.config.dictionaries[]` включает только одно из полей `httpSource`, `mysqlSource`, `clickhouseSource`, `mongodbSource`<br><br>
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>mysqlSource.<br>db | **string**<br><p>Обязательное поле. Имя базы данных MySQL, к которой нужно подключаться.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>mysqlSource.<br>table | **string**<br><p>Обязательное поле. Имя таблицы базы данных, которую следует использовать в качестве словаря ClickHouse.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>mysqlSource.<br>port | **string** (int64)<br><p>Порт по умолчанию, который нужно использовать при подключении к реплике источника словаря.</p> <p>Допустимые значения — от 0 до 65535 включительно.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>mysqlSource.<br>user | **string**<br><p>Имя пользователя по умолчанию для реплик источника словаря.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>mysqlSource.<br>password | **string**<br><p>Пароль пользователя по умолчанию для реплик источника словаря.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>mysqlSource.<br>replicas[] | **object**<br><p>Обязательное поле. Список реплик базы данных MySQL, используемой в качестве источника словаря.</p> <p>Должен содержать хотя бы один элемент.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>mysqlSource.<br>replicas[].<br>host | **string**<br><p>Обязательное поле. Хост реплики MySQL.</p> <p>Максимальная длина строки в символах — 253.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>mysqlSource.<br>replicas[].<br>priority | **string** (int64)<br><p>Обязательное поле. Приоритет реплики, который ClickHouse должен учитывать при подключении. Реплике с наивысшим приоритетом должно соответствовать наименьшее значение в этом поле.</p> <p>Значение должно быть больше 0.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>mysqlSource.<br>replicas[].<br>port | **string** (int64)<br><p>Порт, который нужно использовать при подключении к реплике. Если для какой-либо реплики не указан порт, ClickHouse использует порт, указанный для источника.</p> <p>Допустимые значения — от 0 до 65535 включительно.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>mysqlSource.<br>replicas[].<br>user | **string**<br><p>Имя пользователя базы данных MySQL.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>mysqlSource.<br>replicas[].<br>password | **string**<br><p>Пароль пользователя базы данных MySQL.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>mysqlSource.<br>where | **string**<br><p>Критерии выбора данных в указанной таблице MySQL.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>mysqlSource.<br>invalidateQuery | **string**<br><p>Запрос на проверку состояния словаря, который позволит извлекать только обновленные данные. Дополнительные сведения см. в <a href="https://clickhouse.yandex/docs/en/query_language/dicts/external_dicts_dict_lifetime/">ClickHouse documentation on dictionaries</a>.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>clickhouseSource | **object**<br>ClickHouse-источник для словаря. <br>`configSpec.clickhouse.config.dictionaries[]` включает только одно из полей `httpSource`, `mysqlSource`, `clickhouseSource`, `mongodbSource`<br><br>
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>clickhouseSource.<br>db | **string**<br><p>Обязательное поле. Имя базы данных ClickHouse.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>clickhouseSource.<br>table | **string**<br><p>Обязательное поле. Имя таблицы в указанной базе данных, используемой в качестве источника словаря.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>clickhouseSource.<br>host | **string**<br><p>Обязательное поле. Хост ClickHouse для указанной базы данных.</p> <p>Максимальная длина строки в символах — 253.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>clickhouseSource.<br>port | **string** (int64)<br><p>Порт для подключения к хосту.</p> <p>Допустимые значения — от 0 до 65535 включительно.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>clickhouseSource.<br>user | **string**<br><p>Обязательное поле. Имя пользователя базы данных ClickHouse.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>clickhouseSource.<br>password | **string**<br><p>Пароль пользователя базы данных ClickHouse.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>clickhouseSource.<br>where | **string**<br><p>Критерии выбора данных в указанной таблице ClickHouse.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>mongodbSource | **object**<br>MongoDB-источник для словаря. <br>`configSpec.clickhouse.config.dictionaries[]` включает только одно из полей `httpSource`, `mysqlSource`, `clickhouseSource`, `mongodbSource`<br><br>
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>mongodbSource.<br>db | **string**<br><p>Обязательное поле. Имя базы данных MongoDB.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>mongodbSource.<br>collection | **string**<br><p>Обязательное поле. Имя коллекции в указанной базе данных, которую следует использовать в качестве источника словаря.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>mongodbSource.<br>host | **string**<br><p>Обязательное поле. Хост MongoDB для указанной базы данных.</p> <p>Максимальная длина строки в символах — 253.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>mongodbSource.<br>port | **string** (int64)<br><p>Порт для подключения к хосту.</p> <p>Допустимые значения — от 0 до 65535 включительно.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>mongodbSource.<br>user | **string**<br><p>Обязательное поле. Имя пользователя базы данных MongoDB.</p> 
configSpec.<br>clickhouse.<br>config.<br>dictionaries[].<br>mongodbSource.<br>password | **string**<br><p>Пароль пользователя базы данных MongoDB.</p> 
configSpec.<br>clickhouse.<br>config.<br>graphiteRollup[] | **object**<br><p>Параметры свертки для движка таблицы GraphiteMergeTree.</p> 
configSpec.<br>clickhouse.<br>config.<br>graphiteRollup[].<br>name | **string**<br><p>Обязательное поле. Имя указанной комбинации параметров для свертки Graphite.</p> 
configSpec.<br>clickhouse.<br>config.<br>graphiteRollup[].<br>patterns[] | **object**<br><p>Обязательное поле. Шаблон, используемый для свертки.</p> <p>Должен содержать хотя бы один элемент.</p> 
configSpec.<br>clickhouse.<br>config.<br>graphiteRollup[].<br>patterns[].<br>regexp | **string**<br><p>Шаблон для имен метрик.</p> 
configSpec.<br>clickhouse.<br>config.<br>graphiteRollup[].<br>patterns[].<br>function | **string**<br><p>Обязательное поле. Имя агрегирующей функции, которую следует применить к данным старше возраста, указанного в retention.</p> 
configSpec.<br>clickhouse.<br>config.<br>graphiteRollup[].<br>patterns[].<br>retention[] | **object**<br><p>Обязательное поле. Возраст данных, которые следует использовать для прореживания.</p> <p>Должен содержать хотя бы один элемент.</p> 
configSpec.<br>clickhouse.<br>config.<br>graphiteRollup[].<br>patterns[].<br>retention[].<br>age | **string** (int64)<br><p>Минимальный возраст данных в секундах.</p> <p>Значение должно быть больше 0.</p> 
configSpec.<br>clickhouse.<br>config.<br>graphiteRollup[].<br>patterns[].<br>retention[].<br>precision | **string** (int64)<br><p>Точность определения возраста данных, в секундах.</p> <p>Значение должно быть больше 0.</p> 
configSpec.<br>clickhouse.<br>config.<br>maxConnections | **integer** (int64)<br><p>Максимальное количество входящих подключений.</p> <p>Минимальное значение — 10.</p> 
configSpec.<br>clickhouse.<br>config.<br>maxConcurrentQueries | **integer** (int64)<br><p>Максимальное количество одновременно обрабатываемых запросов.</p> <p>Минимальное значение — 10.</p> 
configSpec.<br>clickhouse.<br>config.<br>keepAliveTimeout | **integer** (int64)<br><p>Количество миллисекунд, в течение которых ClickHouse ожидает входящие запросы прежде чем закрыть подключение.</p> 
configSpec.<br>clickhouse.<br>config.<br>uncompressedCacheSize | **integer** (int64)<br><p>Размер кэша (в байтах) для несжатых данных, используемых таблицами MergeTree. См. подробное описание в <a href="https://clickhouse.yandex/docs/en/operations/server_settings/settings/#uncompressed_cache_size">документации ClickHouse</a>.</p> 
configSpec.<br>clickhouse.<br>config.<br>markCacheSize | **integer** (int64)<br><p>Примерный размер (в байтах) кэша «меток», используемых таблицами MergeTree. Подробнее в <a href="https://clickhouse.yandex/docs/en/operations/server_settings/settings/#mark_cache_size">документации ClickHouse</a>.</p> <p>Значение должно быть больше 5368709120.</p> 
configSpec.<br>clickhouse.<br>config.<br>maxTableSizeToDrop | **integer** (int64)<br><p>Максимальный размер таблицы, которую можно удалить с помощью запроса DROP. См. подробное описание в <a href="https://clickhouse.yandex/docs/en/operations/server_settings/settings/#max_table_size_to_drop">документации ClickHouse</a>.</p> 
configSpec.<br>clickhouse.<br>config.<br>maxPartitionSizeToDrop | **integer** (int64)<br><p>Максимальный размер раздела, который можно удалить с помощью запроса DROP. См. подробное описание в <a href="https://clickhouse.yandex/docs/en/operations/server_settings/settings/#max_partition_size_to_drop">документации ClickHouse</a>.</p> 
configSpec.<br>clickhouse.<br>config.<br>builtinDictionariesReloadInterval | **integer** (int64)<br><p>Интервал времени для перезагрузки встроенных словарей. См. подробное описание в <a href="https://clickhouse.yandex/docs/en/operations/server_settings/settings/#builtin_dictionaries_reload_interval">документации ClickHouse</a>.</p> 
configSpec.<br>clickhouse.<br>config.<br>timezone | **string**<br><p>Часовой пояс сервера, используемый в преобразованиях полей DateTime. Указывается как идентификатор IANA. См. подробное описание в <a href="https://clickhouse.yandex/docs/en/operations/server_settings/settings/#timezone">документации ClickHouse</a>.</p> 
configSpec.<br>clickhouse.<br>resources | **object**<br><p>Ресурсы, выделенные хостам ClickHouse.</p> 
configSpec.<br>clickhouse.<br>resources.<br>resourcePresetId | **string**<br><p>Идентификатор набора вычислительных ресурсов, доступных хосту (процессор, память и т. д.). Все доступные наборы ресурсов перечислены в <a href="/docs/managed-clickhouse/concepts/instance-types">документации</a>.</p> 
configSpec.<br>clickhouse.<br>resources.<br>diskSize | **string** (int64)<br><p>Объем хранилища, доступного хосту, в байтах.</p> 
configSpec.<br>clickhouse.<br>resources.<br>diskTypeId | **string**<br><p>Тип хранилища для хоста. Возможные значения:</p> <ul> <li>network-hdd — сетевой HDD-диск;</li> <li>network-nvme — сетевой SSD-диск;</li> <li>local-nvme — локальное SSD-хранилище.</li> </ul> 
configSpec.<br>zookeeper | **object**<br><p>Конфигурация и ресурсы для сервера ZooKeeper.</p> 
configSpec.<br>zookeeper.<br>resources | **object**<br><p>Ресурсы, выделенные хостам ZooKeeper. Если не задано, будет использоваться минимальный доступный набор ресурсов. Все доступные наборы ресурсов можно получить с помощью запроса <a href="/docs/managed-clickhouse/api-ref/ResourcePreset/list">list</a>.</p> 
configSpec.<br>zookeeper.<br>resources.<br>resourcePresetId | **string**<br><p>Идентификатор набора вычислительных ресурсов, доступных хосту (процессор, память и т. д.). Все доступные наборы ресурсов перечислены в <a href="/docs/managed-clickhouse/concepts/instance-types">документации</a>.</p> 
configSpec.<br>zookeeper.<br>resources.<br>diskSize | **string** (int64)<br><p>Объем хранилища, доступного хосту, в байтах.</p> 
configSpec.<br>zookeeper.<br>resources.<br>diskTypeId | **string**<br><p>Тип хранилища для хоста. Возможные значения:</p> <ul> <li>network-hdd — сетевой HDD-диск;</li> <li>network-nvme — сетевой SSD-диск;</li> <li>local-nvme — локальное SSD-хранилище.</li> </ul> 
configSpec.<br>backupWindowStart | **object**<br><p>Время запуска ежедневного резервного копирования, в часовом поясе UTC.</p> <p>Описывает время суток. Дата и часовой пояс либо не имеют значения, либо указаны другим образом. API может разрешить високосные секунды. Связанные типы: [google.type.Date][google.type.Date] и <code>google.protobuf.Timestamp</code>.</p> 
configSpec.<br>backupWindowStart.<br>hours | **integer** (int32)<br><p>Час в 24-часовом формате. Допустимые значения — от 0 до 23. API может разрешить значение &quot;24:00:00&quot; для таких сценариев, как время закрытия заведения.</p> 
configSpec.<br>backupWindowStart.<br>minutes | **integer** (int32)<br><p>Минута часа. Допустимые значения — от 0 до 59.</p> 
configSpec.<br>backupWindowStart.<br>seconds | **integer** (int32)<br><p>Секунда минуты. Обычно допустимые значения — от 0 до 59. API может разрешить значение 60, если поддерживаются високосные секунды.</p> 
configSpec.<br>backupWindowStart.<br>nanos | **integer** (int32)<br><p>Доли секунды, в наносекундах. Допустимые значения — от 0 до 999 999 999.</p> 
 
## Ответ {#responses}
**HTTP Code: 200 - OK**

```json 
{
  "id": "string",
  "description": "string",
  "createdAt": "string",
  "createdBy": "string",
  "modifiedAt": "string",
  "done": true,
  "metadata": "object",

  //  включает только одно из полей `error`, `response`
  "error": {
    "code": "integer",
    "message": "string",
    "details": [
      "object"
    ]
  },
  "response": "object",
  // конец списка возможных полей

}
```
Ресурс Operation. Дополнительные сведения см. в разделе
[Объект Operation](/docs/api-design-guide/concepts/operation).
 
Поле | Описание
--- | ---
id | **string**<br><p>Идентификатор операции.</p> 
description | **string**<br><p>Описание операции. Длина описания должна быть от 0 до 256 символов.</p> 
createdAt | **string** (date-time)<br><p>Время создания ресурса в формате в <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a>.</p> <p>Строка в формате <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a>.</p> 
createdBy | **string**<br><p>Идентификатор пользователя или сервисного аккаунта, инициировавшего операцию.</p> 
modifiedAt | **string** (date-time)<br><p>Время, когда ресурс Operation последний раз обновлялся. Значение в формате <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a>.</p> <p>Строка в формате <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a>.</p> 
done | **boolean** (boolean)<br><p>Если значение равно <code>false</code> — операция еще выполняется. Если <code>true</code> — операция завершена, и задано значение одного из полей <code>error</code> или <code>response</code>.</p> 
metadata | **object**<br><p>Метаданные операции. Обычно в поле содержится идентификатор ресурса, над которым выполняется операция. Если метод возвращает ресурс Operation, в описании метода приведена структура соответствующего ему поля <code>metadata</code>.</p> 
error | **object**<br>Описание ошибки в случае сбоя или отмены операции. <br> включает только одно из полей `error`, `response`<br><br><p>Описание ошибки в случае сбоя или отмены операции.</p> 
error.<br>code | **integer** (int32)<br><p>Код ошибки. Значение из списка <a href="https://github.com/googleapis/googleapis/blob/master/google/rpc/code.proto">google.rpc.Code</a>.</p> 
error.<br>message | **string**<br><p>Текст ошибки.</p> 
error.<br>details[] | **object**<br><p>Список сообщений с подробными сведениями об ошибке.</p> 
response | **object** <br> включает только одно из полей `error`, `response`<br><br><p>Результат операции в случае успешного завершения. Если исходный метод не возвращает никаких данных при успешном завершении, например метод Delete, поле содержит объект <a href="https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#empty">google.protobuf.Empty</a>. Если исходный метод — это стандартный метод Create / Update, поле содержит целевой ресурс операции. Если метод возвращает ресурс Operation, в описании метода приведена структура соответствующего ему поля <code>response</code>.</p> 