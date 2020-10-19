sequenceDiagram

participant U as User
participant US as User Service
participant BS as Billing Service
participant OS as Order Service 
participant NS as Notification Service

U->>US:POST /users/register
activate US
US->>BS:POST /billing {userId}
activate BS 
BS-->>US: 201 CREATED {billingId}
deactivate BS
US-->>U:201 CREATED
deactivate US
U->>OS:POST /orders
activate OS
OS->>BS:POST /billing/withdraw {userid, sum}
activate BS
BS-->>OS: 200 OK
deactivate BS
OS->>NS:POST /send {templateId, context}
activate NS
NS-->>OS: 202 ACCEPTED
OS-->>U:201 CREATED
deactivate OS
NS-->>NS:sending email
deactivate NS