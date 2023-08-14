# Architectural decisions

| **ID** | **Dates** | **Title** | **Decision** | **References**
| :---: | :---: | :---: | --- | --- |
| AD001 | Jan 1, 2020 | Microservice Configuration Architecture | Implement two types of environment-based configurations: <ol><li>Spring boot profile based with profile specific **application.properties**. This will handle live vs local which allows for running the service outside of a container locally or in another not Kubernetes<sup>®</sup> coupled implementation. </li><li>Implementation of Kubernetes-based configuration using environment properties mapped into the live spring boot profile and stored in config.yaml or passed in via Helm parameters. </li></ol> | <ul><li>[K8's Data Injection](https://kubernetes.io/docs/tasks/inject-data-application/define-command-argument-container/)</li><li>[Spring Boot w K8's properties](https://github.com/fabric8io/spring-cloud-kubernetes#configmap-propertysource)</li><li>[Environment based config options](https://fabric8.io/guide/develop/configuration.html)</li><li>[IBM Example Code](https://github.com/IBM/spring-boot-microservices-on-kubernetes)</li></ul>
| AD002 | Jan 1, 2020 | DNS-based internal referencing | When the custom UIs and services reference each other, they should use the internal service name (this is the name of the Kubernetes service) and port (internally exposed port, for example, 7707) to dynamically reference. This is based on kube-dns. |
| AD003 | Jan 1, 2020 | Spring Boot JSON Library | The decision is to consolidate on the use of GSON and Jackson. To improve performance, use the default approach of GSON for smaller JSON files and Jackson for large JSON files. Although, depending on the service, it may be best to consolidate on just one library for the use case. Jackson is also used for the annotation support. | <ul><li>[Baeldung Jackson vs Gson](http://www.baeldung.com/jackson-vs-gson)</li></li>[The Ultimate Json Library](http://blog.takipi.com/the-ultimate-json-library-json-simple-vs-gson-vs-jackson-vs-json/)</li></ul> |
| AD004 | Jan 1, 2020 | Browser Platform Support | We are currently supporting Chrome, Firefox, and Edge<sup>®</sup>, with limited support for Safari<sup>®</sup>. We do not support any version of Internet Explorer<sup>®</sup> (IE). We typically support the current version and two previous versions. |


## References

1. https://piotrminkowski.wordpress.com/2017/03/31/microservices-with-kubernetes-and-docker/
