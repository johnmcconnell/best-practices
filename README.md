# best-practices
A guide of my best practices

## Best Practices

### 1. A test belongs in the same package/namespace as the source code it is testing

For example, an application that has the directory structure below:

```
  src
   |-erebos
         |- convolution.clj
         |- ica.clj
         |- pca.clj
         |- main.clj
```

should have tests in:

```
  test
   |-erebos
         |- convolution_test.clj
         |- ica_test.clj
         |- pca_test.clj
```

## License

Copyright © 2017 John McConnell

Distributed under the MIT License
