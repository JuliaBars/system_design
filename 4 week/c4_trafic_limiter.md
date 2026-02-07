@startuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml

title Trafic Limiter Schema

Person(customer, "Client", "Uses web browser or mobile app.")

Container(tl, "Trafic Limiter", "", $sprite="elasticsearch")
ContainerDb(query_cache, "Query cache", "Redis", "Counter, timestamp")
ContainerDb(rools_cache, "Rool cache", "Redis", "")
Container(rools_app, "Rools API", "Java/Python/Node", "Business logic")
Container(message_queue, "Message Queue", "RabbitMQ", "")

Container_Boundary(apps, "Api servers") {
    Container(app1, "App Instance 1", "Java/Python/Node", "Business logic")
    Container(app2, "App Instance 2", "Java/Python/Node", "Business logic")
}


' Main flow
Rel(customer, tl, "HTTPS")
Rel(tl, customer, "429: reject query")
Rel(tl, message_queue, "Queued extra queries")
Rel(tl, rools_cache, "HTTPS")
Rel(tl, apps, "HTTPS")
Rel(rools_app, rools_cache,"HTTPS")
Rel(tl, query_cache, "HTTPS", "")

@enduml
