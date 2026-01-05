@startuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml

title Simplified Container diagram with Clusters

Person(customer, "Client", "Uses web browser or mobile app.")

System_Ext(cdn, "CDN", "Content Delivery Network", $sprite="internet")
System_Ext(lb, "Load Balancer", "Distributes traffic", $sprite="elasticsearch")

Container_Boundary(apps, "Application Layer") {
    Container(app1, "App Instance 1", "Java/Python/Node", "Business logic")
    Container(app2, "App Instance 2", "Java/Python/Node", "Business logic")
    Container(app3, "App Instance 3", "Java/Python/Node", "Business logic")
}

Container_Boundary(dbs, "Database Layer") {
    ContainerDb(db_master, "Master", "PostgreSQL", "Write operations")
    ContainerDb(db_replica1, "Replica 1", "PostgreSQL", "Read operations")
    ContainerDb(db_replica2, "Replica 2", "PostgreSQL", "Read operations")
}

Container(cache, "Cache", "Redis", "Session/data cache")
Container(queue, "Message Queue", "RabbitMQ", "Async tasks")
Container(storage, "Object Storage", "S3", "File storage")

' Main flow
Rel(customer, cdn, "HTTPS")
Rel(cdn, lb, "HTTPS")
Rel(lb, apps, "HTTPS")
Rel(apps, dbs, "SQL")
Rel(apps, cache, "Redis protocol")
Rel(apps, queue, "AMQP")
Rel(apps, storage, "S3 API")

' Internal DB replication
Rel(db_master, db_replica1, "Async replication")
Rel(db_master, db_replica2, "Async replication")

@enduml