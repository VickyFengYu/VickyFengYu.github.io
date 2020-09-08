Redis Keyspaces
===================


## <i class="icon-folder-open"></i> Keyspaces

Keyspaces define prefixes used to create the actual key for the Redis Hash. By default, the prefix is set to getClass().getName(). You can alter this default by setting @RedisHash on the aggregate root level or by setting up a programmatic configuration. However, the annotated keyspace supersedes any other configuration.


```
@Configuration
public class MyKeyspaceConfiguration extends KeyspaceConfiguration {

    private long timeToLive = 300l;

    @Bean
    public RedisMappingContext keyValueMappingContext() {
        return new RedisMappingContext(
                new MappingConfiguration(new IndexConfiguration(), new MyKeyspaceConfiguration()));
    }

    @Override
    protected Iterable<KeyspaceSettings> initialConfiguration() {

        KeyspaceSettings keyspace_caseNum = new KeyspaceSettings(RedisRetrieveCaseNum.class, "keyspace-test-1");
        keyspace_caseNum.setTimeToLive(timeToLive);

        KeyspaceSettings keyspace_caseDtls = new KeyspaceSettings(RedisRetrieveCaseDtls.class, "keyspace-test-2");
        keyspace_caseDtls.setTimeToLive(timeToLive);

        Set<KeyspaceSettings> settings = new HashSet<>();
        settings.add(keyspace_caseNum);
        settings.add(keyspace_caseDtls);

        return Collections.unmodifiableSet(settings);
    }

```


## <i class="icon-folder-open"></i> Secondary Indexes

Secondary indexes are used to enable lookup operations based on native Redis structures. Values are written to the according indexes on every save and are removed when objects are deleted or expire.

### <i class="icon-folder-open"></i> Secondary Indexes

Given the sample Person entity shown earlier, we can create an index for firstname by annotating the property with @Indexed

```
@RedisHash("people")
public class Person {

  @Id String id;
  @Indexed String firstname;
  String lastname;
  Address address;
}

```

Indexes are built up for actual property values. Saving two Persons (for example, "rand" and "aviendha") results in setting up indexes similar to the following:

```
SADD people:firstname:rand e2c7dcee-b8cd-4424-883e-736ce564363e
SADD people:firstname:aviendha a9d4b3a0-50d3-4538-a2fc-f7fc2581ee56

```

It is also possible to have indexes on nested elements. Assume Address has a city property that is annotated with @Indexed. In that case, once person.address.city is not null, we have Sets for each city, as shown in the following example:

```
SADD people:address.city:tear e2c7dcee-b8cd-4424-883e-736ce564363e

```



