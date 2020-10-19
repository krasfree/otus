sequenceDiagram

participant U as User
participant G as Gateway
participant MB as Message Broker
participant US as User Service
participant BS as Billing Service
participant OS as Order Service 
participant NS as Notification Service

U->>G: POST /register
activate G
G->>MB: publish
deactivate G
activate MB
note left of US:RegistrationRequest
MB-->>US: consume
deactivate MB

activate US
US->>MB: publish
deactivate US

activate MB
note left of US:UserCreated
MB-->>G:consume

activate G
G-->>U:Response
deactivate G
MB-->>BS: consume
activate BS
deactivate MB
BS->>BS: create user bill
deactivate BS





U->>G:POST /order/create
activate G
G->>MB:publish
deactivate G
activate MB
note left of US:OrderCreateRequest
MB-->>OS:consume
deactivate MB
activate OS

OS->>MB:publish
activate MB

note left of US:OrderCreated
MB-->>G:consume
deactivate MB
activate G
G-->>U: Response
deactivate G

OS->>MB: publish
activate MB
note left of US:PaymentRequest
deactivate OS
MB-->>BS:consume
deactivate MB

activate BS

alt success
BS->>MB:publish
activate MB
note left of US:PaymentSuccess
else failed
BS->>MB:publish
deactivate BS
note left of US:PaymentFailed
end
MB-->>OS:consume
deactivate MB
activate OS
alt success

OS->>MB:publish
activate MB
note left of US:OrderPayed
else failed
OS->>MB:publish
deactivate OS
note left of US:OrderFailed
end
MB-->NS:consume
deactivate MB
activate NS
NS->>NS:send email
deactivate NS