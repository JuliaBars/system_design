@startuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml

title Simplified Container diagram with Clusters

Person(customer, "Client", "Uses web browser or mobile app.")

System_Ext(cdn, "CDN", "Content Delivery Network", $sprite="internet")
System_Ext(lb_2, "Load Balancer", "Distributes traffic", $sprite="internet")
System_Ext(lb, "Database Load Balancer", "Distributes traffic", $sprite="elasticsearch")

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
Rel(customer, lb, "HTTPS")
Rel(lb, apps, "HTTPS")
Rel(apps, lb_2, "SQL")
Rel(lb_2, db_master, "Write")
Rel(lb_2, db_replica1, "Read")
Rel(lb_2, db_replica2, "Read")
Rel(apps, cache, "Redis protocol")
Rel(apps, queue, "AMQP")
Rel(apps, storage, "S3 API")

@enduml
