---
title: Protocolo de mensajería de confianza versión 1,1
ms.date: 03/30/2017
ms.assetid: 0da47b82-f8eb-42da-8bfe-e56ce7ba6f59
ms.openlocfilehash: 349c4dec8f127640d2709abcd63295aace6826df
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2019
ms.locfileid: "64754118"
---
# <a name="reliable-messaging-protocol-version-11"></a>Protocolo de mensajería de confianza versión 1,1

En este tema cubre los detalles de implementación de Windows Communication Foundation (WCF) para el WS-ReliableMessaging protocolo de febrero de 2007 (versión 1.1) necesario para la interoperación mediante el transporte HTTP. WCF sigue la especificación de WS-ReliableMessaging con las restricciones y clarificaciones explicadas en este tema. Tenga en cuenta que la versión 1.1 del protocolo WS-ReliableMessaging se implementa a partir de la [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)].

El WS-ReliableMessaging de febrero de 2007 protocolo se implementa en WCF mediante el <xref:System.ServiceModel.Channels.ReliableSessionBindingElement>.

Para su comodidad, el tema utiliza las siguientes funciones:

- Iniciador: El cliente que inicia la creación de la secuencia de mensajes WS-Reliable.

- Servicio de respuesta: El servicio que recibe las solicitudes del iniciador.

 En este documento, se utilizan los prefijos y espacios de nombres de la tabla siguiente.

|Prefijo|Espacio de nombres|
|-|-|
|wsrm|http://docs.oasis-open.org/ws-rx/wsrm/200702|
|netrm|http://schemas.microsoft.com/ws/2006/05/rm|
|s|http://www.w3.org/2003/05/soap-envelope|
|wsa|http://schemas.xmlsoap.org/ws/2005/08/addressing|
|wsse|http://docs.oasis-open.org/wss/2004/01/oasis-200401-wssecurity-secext-1.0.xsd|
|wsrmp|http://docs.oasis-open.org/ws-rx/wsrmp/200702|
|netrmp|http://schemas.microsoft.com/ws-rx/wsrmp/200702|
|wsp|(Directiva WS-Policy 1.2 o WS-Policy 1.5)|

## <a name="messaging"></a>Mensajería

### <a name="sequence-creation"></a>Creación de secuencias

WCF implementa `CreateSequence` y `CreateSequenceResponse` de secuencia de mensajes para establecer una mensajería confiable. Las siguientes restricciones son aplicables:

- B1101: El iniciador de WCF usa la misma referencia de punto de conexión como el `CreateSequence` del mensaje `ReplyTo`, `AcksTo` y `Offer/Endpoint`.

- R1102: El `AcksTo`, `ReplyTo` y `Offer/Endpoint` hace referencia un punto de conexión en el `CreateSequence` mensaje debe tener los valores de dirección con representaciones de cadena idénticas, que coincidan byte a byte.

  - El servicio de respuesta WCF comprueba que la parte del URI del `AcksTo`, `ReplyTo` y `Endpoint` las referencias de extremo son idénticas antes de crear una secuencia.

- R1103: El `AcksTo`, `ReplyTo` y `Offer/Endpoint` hace referencia un punto de conexión en el `CreateSequence` mensaje debe tener el mismo conjunto de parámetros de referencia.

  - WCF no exige, pero se da por supuesto que hacen referencia a parámetros de la `AcksTo`, `ReplyTo` y `Offer/Endpoint` hace referencia un punto de conexión en `CreateSequence` son idénticas y utiliza los parámetros de referencia desde el `ReplyTo` referencia del extremo para las confirmaciones y los mensajes de secuencia inversa.

- B1104: El iniciador de WCF no genera opcional `Expires` o `Offer/Expires` elemento en el `CreateSequence` mensaje.

- B1105: Al obtener acceso a la `CreateSequence` mensaje, el servicio de respuesta WCF usa la `Expires` valor en el `CreateSequence` elemento como el `Expires` valor en el `CreateSequenceResponse` elemento. En caso contrario, el servicio de respuesta WCF lee y pasa por alto el `Expires` y `Offer/Expires` valores.

- B1106: Al obtener acceso a la `CreateSequenceResponse` mensaje, el iniciador de WCF lee el elemento opcional `Expires` valor pero no lo usa.

- B1107: El iniciador de WCF y el contestador siempre generan opcional `IncompleteSequenceBehavior` elemento en el `CreateSequence/Offer` y `CreateSequenceResponse` elementos.

- B1108: WCF usa sólo el `DiscardFollowingFirstGap` y `NoDiscard` valores en el `IncompleteSequenceBehavior` elemento.

  - WS-ReliableMessaging utiliza el mecanismo `Offer` para establecer las dos secuencias correlacionadas inversas que forman una sesión.

- B1109: Si `CreateSequence` contiene un `Offer` elemento, el Respondedor unidireccional de WCF rechaza la secuencia proporcionada respondiendo con un `CreateSequenceResponse` sin un `Accept` elemento.

- B1110: Si un Respondedor de mensajería de confianza rechaza la secuencia proporcionada, el iniciador de WCF produce un error en la secuencia recientemente establecida.

- B1111: Si `CreateSequence` no contiene un `Offer` elemento, el Respondedor bidireccional de WCF rechaza la secuencia proporcionada respondiendo con un `CreateSequenceRefused` error.

- R1112: Cuando dos secuencias inversas se establecen utilizando el `Offer` mecanismo, el `[address]` propiedad de la `CreateSequenceResponse/Accept/AcksTo` referencia de punto de conexión debe coincidir con el URI de destino de la `CreateSequence` byte a byte mensaje.

- R1113: Cuando dos secuencias inversas se establecen utilizando el `Offer` mecanismo, todos los mensajes en ambas secuencias que fluyen desde el iniciador al Respondedor se deben enviar a la misma referencia de punto de conexión.

WCF usa WS-ReliableMessaging para establecer sesiones confiables entre el iniciador y el Respondedor. La implementación de WCF WS-ReliableMessaging proporciona una sesión confiable para completa y de solicitud-respuesta unidireccional, patrones de mensajería dúplex. El mecanismo `Offer` de WS-ReliableMessaging en `CreateSequence` y `CreateSequenceResponse` le permite establecer dos secuencias inversas correlacionadas y proporciona un protocolo de sesión que es apto para todos los puntos de conexión de mensajes. Dado que WCF proporciona una garantía de seguridad para este tipo de sesión incluida la protección de extremo a otro para la integridad de la sesión, es práctico para asegurarse de que los mensajes destinados a la misma parte lleguen al mismo destino. Esto también permite el “apoyo a caballo” de confirmaciones de secuencias en mensajes de aplicaciones. Por lo tanto, se aplican restricciones R1102 R1112 y R1113 a WCF.

Ejemplo de mensaje `CreateSequence`.

```xml
<s:Envelope>
  <s:Header>
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/CreateSequence</wsa:Action>
    <wsa:MessageID>urn:uuid:949cca61-8813-42ff-ab33-18d9e3fa82fa</wsa:MessageID>
    <wsa:ReplyTo>
        <wsa:Address>http://Business456.com/clientA</wsa:Address>
    </wsa:ReplyTo>
    <wsa:To s:mustUnderstand="1">http://BusinessABC.com/serviceA</wsa:To>
  </s:Header>
  <s:Body>
    <wsrm:CreateSequence>
      <wsrm:AcksTo>
        <wsa:Address>http://Business456.com/clientA</wsa:Address>
      </wsrm:AcksTo>
      <wsrm:Offer>
        <wsrm:Identifier>urn:uuid:066b4730-fc82-458a-a5c1-210be4fb4e4e</wsrm:Identifier>
        <wsrm:Endpoint>
          <wsa:Address>http://Business456.com/clientA</wsa:Address>
        </wsrm:Endpoint>
        <wsrm:IncompleteSequenceBehavior>DiscardFollowingFirstGap</wsrm:IncompleteSequenceBehavior>
      </wsrm:Offer>
    </wsrm:CreateSequence>
  </s:Body>
</s:Envelope>
```

Ejemplo de mensaje `CreateSequenceResponse`.

```xml
<s:Envelope>
  <s:Header>
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/CreateSequenceResponse</wsa:Action>
    <wsa:RelatesTo>urn:uuid:949cca61-8813-42ff-ab33-18d9e3fa82fa</wsa:RelatesTo>
    <wsa:To s:mustUnderstand="1">http://Business456.com/clientA</wsa:To>
  </s:Header>
  <s:Body>
    <wsrm:CreateSequenceResponse>
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
      <wsrm:IncompleteSequenceBehavior>DiscardFollowingFirstGap</wsrm:IncompleteSequenceBehavior>
      <wsrm:Accept>
        <wsrm:AcksTo>
          <wsa:Address>http://BusinessABC.com/serviceA</wsa:Address>
        </wsrm:AcksTo>
      </wsrm:Accept>
    </wsrm:CreateSequenceResponse>
  </s:Body>
</s:Envelope>
```

### <a name="closing-a-sequence"></a>Cierre de una secuencia

WCF usa la `CloseSequence` y `CloseSequenceResponse` mensajes para un apagado iniciada por el origen de mensajería de confianza. El destino de mensajería confiable de WCF no inicia el cierre y el origen de mensajería confiable de WCF no admite un cierre iniciado por el destino de mensajería de confianza. Las siguientes restricciones son aplicables:

- B1201: El origen de mensajería confiable de WCF siempre envía un `CloseSequence` mensaje para cerrar la secuencia.

- B1202: El origen de mensajería de confianza espera la confirmación de la gama completa de los mensajes de secuencia antes de enviar el `CloseSequence` mensaje.

- B1203: El origen de mensajería de confianza siempre incluye el elemento opcional `LastMsgNumber` elemento a menos que la secuencia no contiene mensajes.

- R1204: El destino de mensajería de confianza no debe iniciar el apagado enviando un `CloseSequence` mensaje.

- B1205: Una vez recibida una `CloseSequence` mensaje, el origen de mensajería confiable de WCF considera la secuencia incompleta y envía un error.

 Ejemplo de mensaje `CloseSequence`.

```xml
<s:Envelope>
  <s:Header>
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/CloseSequence</wsa:Action>
    <wsa:MessageID>urn:uuid:6ce1d4c3-e1c1-474f-a8c9-4210e37f7877</wsa:MessageID>
    <wsa:ReplyTo>
      <wsa:Address>http://Business456.com/clientA</wsa:Address>
    </wsa:ReplyTo>
    <wsa:To s:mustUnderstand="1">http://BusinessABC.com/serviceA</wsa:To>
  </s:Header>
  <s:Body>
    <wsrm:CloseSequence>
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
      <wsrm:LastMsgNumber>30</wsrm:LastMsgNumber>
    </wsrm:CloseSequence>
  </s:Body>
</s:Envelope>
```

Ejemplo `CloseSequenceResponse` mensaje:

```xml
<s:Envelope>
  <s:Header>
    <wsrm:SequenceAcknowledgement>
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
      <wsrm:AcknowledgementRange Lower="1" Upper="30"></wsrm:AcknowledgementRange>
      <wsrm:Final></wsrm:Final>
      <netrm:BufferRemaining>8</netrm:BufferRemaining>
    </wsrm:SequenceAcknowledgement>
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/CloseSequenceResponse</wsa:Action>
    <wsa:RelatesTo>urn:uuid:6ce1d4c3-e1c1-474f-a8c9-4210e37f7877</wsa:RelatesTo>
    <wsa:To s:mustUnderstand="1">http://Business456.com/clientA</wsa:To>
  </s:Header>
  <s:Body>
    <wsrm:CloseSequenceResponse>
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
    </wsrm:CloseSequenceResponse>
  </s:Body>
</s:Envelope>
```

### <a name="sequence-termination"></a>Finalización de secuencia

WCF usa principalmente el `TerminateSequence/TerminateSequenceResponse` protocolo de enlace después de completar la `CloseSequence/CloseSequenceResponse` protocolo de enlace. El destino de mensajería confiable de WCF no inicia la finalización y el origen de mensajería de confianza no admite una terminación iniciada por el destino de mensajería de confianza. Las siguientes restricciones son aplicables:

- B1301: El iniciador de WCF solo envía el `TerminateSequence` mensaje tras la finalización correcta de la `CloseSequence/CloseSequenceResponse` protocolo de enlace.

- R1302: WCF valida que el `LastMsgNumber` elemento sea coherente en todos los `CloseSequence` y `TerminateSequence` mensajes para una secuencia determinada. Esto significa que `LastMsgNumber` no está presente en todos los mensajes `CloseSequence` y `TerminateSequence`, o está presente y es idéntico en todos los mensajes `CloseSequence` y `TerminateSequence`.

- B1303: Cuando se recibe un `TerminateSequence` mensaje después de la `CloseSequence/CloseSequenceResponse` protocolo de enlace, el destino de mensajería de confianza responde con un `TerminateSequenceResponse` mensaje. Puesto que el origen de la mensajería de confianza recibe la confirmación definitiva antes de enviar el mensaje `TerminateSequence`, el destino de la mensajería de confianza sabe sin duda que finaliza la secuencia y reclama recursos inmediatamente.

- B1304: Cuando se recibe un `TerminateSequence` mensajes anteriores a la `CloseSequence/CloseSequenceResponse` protocolo de enlace, el destino de mensajería confiable de WCF responde con un `TerminateSequenceResponse` mensaje. Si el destino de la mensajería de confianza determina que no hay incoherencias en la secuencia, el destino de la mensajería de confianza espera durante un tiempo especificado por el destino de la aplicación antes de reclamar recursos, para permitir al cliente que reciba la confirmación final. De lo contrario, el destino de la mensajería de confianza reclama recursos inmediatamente e indica al destino de la aplicación que la secuencia finaliza de manera dudosa iniciando el evento `Faulted`.

Ejemplo de mensaje `TerminateSequence`.

```xml
<s:Envelope>
  <s:Header>
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/TerminateSequence</wsa:Action>
    <wsa:MessageID>urn:uuid:3597a398-4f3c-40f4-9335-8f1515572fdf</wsa:MessageID>
    <wsa:ReplyTo>
      <wsa:Address>http://Business456.com/clientA</wsa:Address>
    </wsa:ReplyTo>
    <wsa:To s:mustUnderstand="1">http://BusinessABC.com/serviceA</wsa:To>
  </s:Header>
  <s:Body>
    <wsrm:TerminateSequence>
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
      <wsrm:LastMsgNumber>30</wsrm:LastMsgNumber>
      </wsrm:TerminateSequence>
  </s:Body>
</s:Envelope>
```

Ejemplo `TerminateSequenceResponse` mensaje:

```xml
<s:Envelope>
  <s:Header>
    <wsrm:SequenceAcknowledgement>
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
      <wsrm:AcknowledgementRange Lower="1" Upper="30"></wsrm:AcknowledgementRange>
      <wsrm:Final></wsrm:Final>
      <netrm:BufferRemaining>8</netrm:BufferRemaining>
    </wsrm:SequenceAcknowledgement>
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/TerminateSequenceResponse</wsa:Action>
    <wsa:RelatesTo>urn:uuid:3597a398-4f3c-40f4-9335-8f1515572fdf</wsa:RelatesTo>
    <wsa:To s:mustUnderstand="1">://Business456.com/clientA</wsa:To>
  </s:Header>
  <s:Body>
    <wsrm:TerminateSequenceResponse>
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
    </wsrm:TerminateSequenceResponse>
  </s:Body>
</s:Envelope>
```

### <a name="sequences"></a>Secuencias

A continuación, se muestra una lista de restricciones que se aplican a las secuencias:

- Genera B1401:WCF y no mayores que los números de secuencia de accesos `xs:long`del valor inclusivo máximo, 9223372036854775807.

Ejemplo de encabezado `Sequence`.

```xml
<wsrm:Sequence s:mustUnderstand="1">
  <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
  <wsrm:MessageNumber>1</wsrm:MessageNumber>
</wsrm:Sequence>
```

### <a name="request-acknowledgement"></a>Solicitar confirmación

WCF usa la `AckRequested` encabezado como un mecanismo keep-alive.

Ejemplo de encabezado `AckRequested`.

```xml
<wsrm:AckRequested>
  <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
</wsrm:AckRequested>
```

### <a name="sequenceacknowledgement"></a>SequenceAcknowledgement

WCF usa un mecanismo de "apoyo a caballo" de confirmaciones de secuencias proporcionadas en WS-Reliable Messaging. Las siguientes restricciones son aplicables:

- R1601: Cuando dos secuencias inversas se establecen utilizando el `Offer` mecanismo, el `SequenceAcknowledgement` encabezado puede incluirse en cualquier mensaje de aplicación transmitido al destinatario deseado. El extremo remoto debe poder tener acceso a un encabezado `SequenceAcknowledgement` superpuesto.

- B1602: WCF no genera `SequenceAcknowledgement` los encabezados que contienen `Nack` elementos. WCF valida que cada `Nack` elemento contiene un número de secuencia, pero en caso contrario, se omite el `Nack` elemento y el valor.

 Ejemplo de encabezado `SequenceAcknowledgement`.

```xml
<wsrm:SequenceAcknowledgement>
  <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
  <wsrm:AcknowledgementRange Lower="1" Upper="1"></wsrm:AcknowledgementRange>
</wsrm:SequenceAcknowledgement>
```

### <a name="ws-reliablemessaging-faults"></a>Errores de WS-ReliableMessaging

La siguiente es una lista de restricciones que se aplican a la implementación de WCF de WS-ReliableMessaging errores. Las siguientes restricciones son aplicables:

- B1701: WCF no genera `MessageNumberRollover` errores.

- B1702: A través de SOAP 1.2, cuando el punto de conexión de servicio alcanza su límite de conexión y no puede procesar nuevas conexiones, WCF genera anidada `CreateSequenceRefused` subcódigo, de error `netrm:ConnectionLimitReached`, como se muestra en el ejemplo siguiente.

```xml
<s:Envelope>
  <s:Header>
    <wsa:Action>http://docs.oasis-open.org/ws-rx/wsrm/200702/fault</wsa:Action>
  </s:Header>
  <s:Body>
    <s:Fault>
      <s:Code>
        <s:Value>s:Receiver</s:Value>
        <s:Subcode>
          <s:Value>wsrm:CreateSequenceRefused</s:Value>
          <s:Subcode>
            <s:Value>netrm:ConnectionLimitReached</s:Value>
          </s:Subcode>
        </s:Subcode>
      </s:Code>
      <s:Reason>
        <s:Text xml:lang="en">Server 'http://BusinessABC.com/serviceA' is too busy to process this request. Try again later.</s:Text>
      </s:Reason>
    </s:Fault>
  </s:Body>
</s:Envelope>
```

### <a name="ws-addressing-faults"></a>Errores WS-Addressing

Dado que WS-ReliableMessaging utiliza WS-Addressing, la implementación de WCF WS-ReliableMessaging puede generar y transmitir errores de WS-Addressing. En esta sección se trata los errores de WS-Addressing que WCF genera explícitamente y transmite en el nivel de WS-ReliableMessaging:

- B1801:WCF genera y transmite el `Message Addressing Header Required` de error cuando se cumple una de las siguientes acciones:

  - A un mensaje `CreateSequence`, `CloseSequence`, o `TerminateSequence` le falta un encabezado `MessageId`.

  - A un mensaje `CreateSequence`, `CloseSequence`, o `TerminateSequence` le falta un encabezado `ReplyTo`.

  - A un mensaje `CreateSequenceResponse`, `CloseSequenceResponse`, o `TerminateSequenceResponse` le falta un encabezado `RelatesTo`.

- B1802:WCF genera y transmite el `Endpoint Unavailable` error para indicar que no hay ningún extremo escuchando que puede procesar la secuencia basada en el examen de los encabezados de direccionamiento del `CreateSequence` mensaje.

## <a name="protocol-composition"></a>Composición de protocolos

### <a name="composition-with-ws-addressing"></a>Composición con WS-Addressing

WCF admite dos versiones de WS-Addressing: WS-Addressing 2004/08 [WS-ADDR] y W3C WS-Addressing 1.0 recomendaciones [WS-ADDR-CORE] y [WS-ADDR-SOAP].

Aunque la especificación de WS-ReliableMessaging solo menciona WS-Addressing 2004/08, no restringe la versión de WS-Addressing que se ha de utilizar. La siguiente es una lista de restricciones que se aplican a WCF:

- R2101: WS-Addressing 2004/08 y WS-Addressing 1.0 se pueden usar con WS-Reliable Messaging.

- R2102: Se debe usar una única versión de WS-Addressing a lo largo de una secuencia WS-ReliableMessaging determinada o un par de secuencias inversas correlacionadas mediante el `Offer` mecanismo.

### <a name="composition-with-soap"></a>Composición con SOAP

WCF admite el uso de SOAP 1.1 y SOAP 1.2 con WS-Reliable Messaging.

### <a name="composition-with-ws-security-and-ws-secureconversation"></a>Composición con WS-Security y WS-SecureConversation

WCF proporciona protección para secuencias WS-ReliableMessaging mediante el uso de transporte (HTTPS) segura, la composición con WS-Security y composición con WS-Secure Conversation. Los protocolos WS-ReliableMessaging 1.1, WS-Security 1.1 y WS-Secure Conversation 1.3 deberían utilizarse conjuntamente. La siguiente es una lista de restricciones que se aplican a WCF:

- R2301: Para proteger la integridad de una secuencia WS-ReliableMessaging además de la integridad y confidencialidad de los mensajes individuales, WCF requiere que se deben utilizar WS-Secure Conversation.

- R2302:AWS-Secure Conversation debe establecerse antes de establecer las secuencias de WS-ReliableMessaging.

- R2303: Si la duración de la secuencia WS-ReliableMessaging supera WS-Secure Conversation, la duración de la sesión, el `SecurityContextToken` establecido mediante WS-Secure Conversation se debe renovar utilizando el enlace de renovación WS-Secure Conversation correspondiente.

- B2304:WS-ReliableMessaging secuencia o un par de secuencias inversas correlacionadas siempre se enlazan a una sola sesión de WS-SecureConversation.

- R2305: Cuando se compone con WS-Secure Conversation, el servicio de respuesta WCF requiere que el `CreateSequence` mensaje contienen el `wsse:SecurityTokenReference` elemento y el `wsrm:UsesSequenceSTR` encabezado.

 Ejemplo de encabezado `UsesSequenceSTR`.

```xml
<wsrm:UsesSequenceSTR></wsrm:UsesSequenceSTR>
```

### <a name="composition-with-ssltls-sessions"></a>Composición con sesiones de SSL/TLS

WCF no admite la composición con sesiones SSL/TLS:

- B2401: WCF no genera el `wsrm:UsesSequenceSSL` encabezado.

- R2402: No debe enviar un iniciador de la mensajería confiable un `CreateSequence` del mensaje con un `wsrm:UsesSequenceSSL` encabezado a un servicio de respuesta WCF.

### <a name="composition-with-ws-policy"></a>Composición con WS-Policy

WCF admite dos versiones de WS-Policy: WS-Policy 1.2 y WS-Policy 1.5.

## <a name="ws-reliablemessaging-ws-policy-assertion"></a>Aserción de WS-Policy de WS-ReliableMessaging 

WCF usa la aserción de WS-Policy WS-ReliableMessaging `wsrm:RMAssertion` para describir funciones de extremos. La siguiente es una lista de restricciones que se aplican a WCF:

- B3001: WCF adjunta `wsrmn:RMAssertion` WS-Policy Assertion a `wsdl:binding` elementos. WCF admite datos adjuntos a `wsdl:binding` y `wsdl:port` elementos.

- B3002: WCF nunca genera la `wsp:Optional` etiqueta.

- B3003: Al obtener acceso a la `wsrmp:RMAssertion` aserción de WS-Policy, WCF omite el `wsp:Optional` etiquetar y trata la directiva WS-RM como obligatorio.

- R3004: Dado que WCF no compone con sesiones de SSL/TLS, WCF no acepta la directiva que especifica `wsrmp:SequenceTransportSecurity`.

- B3005: WCF siempre genera el `wsrmp:DeliveryAssurance` elemento.

- B3006: WCF siempre especifica el `wsrmp:ExactlyOnce` garantía de entrega.

- B3007: WCF genera y lee las siguientes propiedades de la aserción WS-ReliableMessaging y proporciona control sobre ellas en WCF`ReliableSessionBindingElement`:

  - `netrmp:InactivityTimeout`

  - `netrmp:AcknowledgementInterval`

  Ejemplo de `RMAssertion`.

  ```xml
  <wsrmp:RMAssertion>
    <wsp:Policy>
      <wsrmp:SequenceSTR/>
      <wsrmp:DeliveryAssurance>
        <wsp:Policy>
          <wsrmp:ExactlyOnce/>
          <wsrmp:InOrder/>
        </wsp:Policy>
      </wsrmp:DeliveryAssurance>
    </wsp:Policy>
    <netrmp:InactivityTimeout Milliseconds="600000"/>
    <netrmp:AcknowledgementInterval Milliseconds="200"/>
  </wsrmp:RMAssertion>
  ```

## <a name="flow-control-ws-reliablemessaging-extension"></a>Extensión de WS-ReliableMessaging de control de flujo

WCF usa WS-ReliableMessaging extensibilidad para proporcionar un control más estricto adicional opcional sobre el flujo de mensajes de secuencias.

Control de flujo se habilita estableciendo el <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.FlowControlEnabled?displayProperty=nameWithType> propiedad `true`. La siguiente es una lista de restricciones que se aplican a WCF:

- B4001: Cuando está habilitado el Control de flujo de mensajería confiable, WCF genera un `netrm:BufferRemaining` elemento en la extensibilidad de elementos de la `SequenceAcknowledgement` encabezado, tal como se muestra en el ejemplo siguiente.

  ```xml
  <wsrm:SequenceAcknowledgement>
    <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
    <wsrm:AcknowledgementRange Upper="1" Lower="1"/>
    <netrm:BufferRemaining>8</netrm:BufferRemaining>
  </wsrm:SequenceAcknowledgement>
  ```

- B4002: Incluso cuando está habilitado Control de flujo de mensajería confiable, WCF no requieren un `netrm:BufferRemaining` elemento en el `SequenceAcknowledgement` encabezado.

- B4003: Destino de mensajería confiable de WCF usa `netrm:BufferRemaining` indicar cuántos mensajes nuevos puede almacenar en búfer.

- B4004:when Reliable Messaging de flujo de Control está habilitado, el origen de mensajería confiable de WCF usa el valor de `netrm:BufferRemaining` para la transmisión de mensajes del acelerador.

- B4005: WCF genera `netrm:BufferRemaining` entero valores entre 0 y 4.096, ambos incluidos y lee valores enteros entre 0 y `xs:int`del `maxInclusive` valor 214748364 inclusive.

## <a name="message-exchange-patterns"></a>Modelos de intercambio de mensajes

Esta sección describe el comportamiento de WCF cuando se usa WS-ReliableMessaging para diferentes patrones de intercambio de mensajes. Para cada patrón de intercambio de mensajes, se consideran los dos escenarios de implementación siguientes:

- Iniciador no direccionable: Iniciador está tras un firewall; Servicio de respuesta puede entregar mensajes al iniciador sólo en las respuestas HTTP.

- Iniciador direccionable: Iniciador y Respondedor se pueden enviar solicitudes HTTP; en otras palabras, se pueden establecer dos conexiones HTTP inversas.

### <a name="one-way-non-addressable-initiator"></a>Iniciador unidireccional no direccionable

#### <a name="binding"></a>Enlaces

WCF proporciona un patrón de intercambio de mensajes unidireccional utilizando una secuencia sobre un canal HTTP. WCF usa solicitudes HTTP para transmitir todos los mensajes desde el iniciador hasta el Respondedor y respuestas HTTP para transmitir todos los mensajes desde el servicio de respuesta al iniciador.

#### <a name="createsequence-exchange"></a>Intercambio de CreateSequence

El iniciador de WCF transmite un `CreateSequence` mensaje sin ningún `Offer` elemento en una solicitud HTTP y espera el `CreateSequenceResponse` mensaje en la respuesta HTTP. El servicio de respuesta WCF crea una secuencia y transmite el `CreateSequenceResponse` mensaje sin ningún `Accept` elemento en la respuesta HTTP.

#### <a name="sequenceacknowledgement"></a>SequenceAcknowledgement

El iniciador de WCF procesa las confirmaciones en la respuesta de todos los mensajes excepto el `CreateSequence` mensajes y mensajes de error. El servicio de respuesta WCF siempre transmite una confirmación independiente en la respuesta HTTP a todas las secuencia y `AckRequested` mensajes.

#### <a name="closesequence-exchange"></a>Intercambio de CloseSequence

El iniciador de WCF transmite un `CloseSequence` del mensaje en una solicitud HTTP y espera el `CreateSequenceResponse` mensaje en la respuesta HTTP. El servicio de respuesta WCF transmite el `CloseSequenceResponse` mensaje en la respuesta HTTP.

#### <a name="terminatesequence-exchange"></a>Intercambio de TerminateSequence

El iniciador de WCF transmite un `TerminateSequence` del mensaje en una solicitud HTTP y espera el `TerminateSequenceResponse` mensaje en la respuesta HTTP. El servicio de respuesta WCF transmite el `TerminateSequenceResponse` mensaje en la respuesta HTTP.

### <a name="one-way-addressable-initiator"></a>Iniciador unidireccional y direccionable

#### <a name="binding"></a>Enlaces

WCF proporciona un patrón de intercambio de mensajes unidireccional utilizando una secuencia sobre una entrada y un canal HTTP saliente. WCF usa las solicitudes HTTP para transmitir todos los mensajes. Todas las respuestas HTTP tienen un cuerpo vacío y código de estado HTTP 202.

#### <a name="createsequence-exchange"></a>Intercambio de CreateSequence

El iniciador de WCF transmite un `CreateSequence` mensaje sin ningún `Offer` elemento en una solicitud HTTP. El servicio de respuesta WCF crea una secuencia y transmite el `CreateSequenceResponse` mensaje sin ningún `Accept` elemento en una solicitud HTTP.

### <a name="duplex-addressable-initiator"></a>Iniciador dúplex y direccionable

#### <a name="binding"></a>Enlaces

WCF proporciona un patrón de intercambio de mensajes totalmente asincrónico y bidireccional utilizando dos secuencias sobre un entrante y un canal HTTP saliente. Este patrón de intercambio de mensajes se puede mezclar con el patrón de intercambio de mensajes del iniciador de `Request/Reply`, `Addressable` de una manera limitada. WCF usa solicitudes HTTP para transmitir todos los mensajes. Todas las respuestas HTTP tienen un cuerpo vacío y código de estado HTTP 202.

#### <a name="createsequence-exchange"></a>Intercambio de CreateSequence

El iniciador de WCF transmite un `CreateSequence` del mensaje con un `Offer` elemento en una solicitud HTTP. El servicio de respuesta WCF garantiza que el `CreateSequence` tiene un `Offer` elemento, a continuación, crea una secuencia y transmite el `CreateSequenceResponse` del mensaje con un `Accept` elemento.

#### <a name="sequence-lifetime"></a>Duración de la secuencia

WCF trata las dos secuencias como una sesión totalmente dúplex.

Tras generar un error que se produce un error en una secuencia, WCF espera que el extremo remoto al error en ambas secuencias. Tras leer un error que se produce un error en una secuencia, WCF produce un error en ambas secuencias.

WCF puede cerrar su secuencia saliente y continuar procesando los mensajes en su secuencia entrante. Por el contrario, WCF puede procesar el cierre de la secuencia entrante y continuar enviando mensajes en su secuencia saliente.

### <a name="request-reply-and-one-way-non-addressable-initiator"></a>Iniciador de solicitud-respuesta unidireccional y no direccionable

#### <a name="binding"></a>Enlaces

WCF ofrece un sentido y patrón de intercambio de mensajes de solicitud-respuesta usando dos secuencias sobre un canal HTTP. WCF usa solicitudes HTTP para transmitir todos los mensajes desde el iniciador hasta el Respondedor y respuestas HTTP para transmitir todos los mensajes desde el servicio de respuesta al iniciador.

#### <a name="createsequence-exchange"></a>Intercambio de CreateSequence

El iniciador de WCF transmite un `CreateSequence` del mensaje con un `Offer` elemento en una solicitud HTTP y espera el `CreateSequenceResponse` mensaje en la respuesta HTTP. El servicio de respuesta WCF crea una secuencia y transmite el `CreateSequenceResponse` del mensaje con un `Accept` elemento en la respuesta HTTP.

#### <a name="one-way-message"></a>Mensaje unidireccional

Para completar correctamente un intercambio de mensajes unidireccional, el iniciador de WCF transmite un mensaje de secuencia de solicitud en la solicitud HTTP y recibe una independiente `SequenceAcknowledgement` mensaje en la respuesta HTTP. La `SequenceAcknowledgement` debe confirmar el mensaje transmitido.

El servicio de respuesta WCF puede responder a la solicitud con una confirmación, un error o una respuesta con un cuerpo vacío y el código de estado HTTP 202.

#### <a name="two-way-messages"></a>Mensajes bidireccionales

Para completar correctamente un protocolo de intercambio de mensajes bidireccional, el iniciador de WCF transmite un mensaje de secuencia de solicitud en la solicitud HTTP y recibe un mensaje de secuencia de respuesta en la respuesta HTTP. La respuesta debe llevar una `SequenceAcknowledgement` que confirme que se ha transmitido el mensaje de secuencia de solicitud.

El servicio de respuesta WCF puede responder a la solicitud con una respuesta de la aplicación, un error o una respuesta con un cuerpo vacío y el código de estado HTTP 202.

Debido a la presencia de mensajes unidireccionales y al control de tiempo de las respuestas de la aplicación, el número de secuencia del mensaje de secuencia de solicitud y el número de secuencia del mensaje de respuesta no tienen ninguna correlación.

#### <a name="retrying-replies"></a>Reintento de respuestas

WCF se basa en la correlación de solicitud-respuesta HTTP para la correlación de protocolo de intercambio de mensajes bidireccional. Por este motivo, el iniciador de WCF no deja de reintentar un mensaje de secuencia de solicitud cuando se confirma el mensaje de secuencia de solicitud, sino cuando la respuesta HTTP lleva una `SequenceAcknowledgement`, respuesta de la aplicación o error. El servicio de respuesta WCF reintenta las respuestas en la respuesta HTTP de la solicitud a la que se correlaciona la respuesta.

#### <a name="closesequence-exchange"></a>Intercambio de CloseSequence

Después de recibir todos los mensajes de secuencia de respuesta y confirmaciones para todos los mensajes de secuencia de solicitud unidireccional, el iniciador de WCF transmite un `CloseSequence` del mensaje para la secuencia de solicitud en una solicitud HTTP y espera el `CloseSequenceResponse` en la respuesta HTTP.

Al cerrar implícitamente la secuencia de la solicitud, se cierra la secuencia de la respuesta. Esto significa que el iniciador de WCF incluye Final la secuencia de respuesta `SequenceAcknowledgement` en el `CloseSequence` mensaje y la secuencia de respuesta no tiene un `CloseSequence` exchange.

El servicio de respuesta WCF garantiza que todas las respuestas se confirmen y transmite el `CloseSequenceResponse` mensaje en la respuesta HTTP.

#### <a name="terminatesequence-exchange"></a>Intercambio de TerminateSequence

Después de recibir el `CloseSequenceResponse` mensaje, el iniciador de WCF transmite un `TerminateSequence` del mensaje para la secuencia de solicitud en una solicitud HTTP y espera el `TerminateSequenceResponse` en la respuesta HTTP.

Al igual que en el intercambio de `CloseSequence`, al finalizar la secuencia de solicitud, se finaliza la secuencia de respuesta. Esto significa que el iniciador de WCF incluye final de la secuencia de respuesta `SequenceAcknowledgement` en el `TerminateSequence` mensaje y la secuencia de respuesta no tiene un `TerminateSequence` exchange.

El servicio de respuesta WCF transmite el `TerminateSequenceResponse` mensaje en la respuesta HTTP.

### <a name="requestreply-addressable-initiator"></a>Iniciador direccionable de solicitud-respuesta

#### <a name="binding"></a>Enlaces

WCF proporciona un patrón de intercambio de mensajes de solicitud-respuesta usando dos secuencias sobre un entrante y un canal HTTP saliente. Este patrón de intercambio de mensajes se puede mezclar con el patrón de intercambio de mensajes del iniciador de `Duplex, Addressable` de una manera limitada. WCF usa las solicitudes HTTP para transmitir todos los mensajes. Todas las respuestas HTTP tienen un cuerpo vacío y código de estado HTTP 202.

#### <a name="createsequence-exchange"></a>Intercambio de CreateSequence

El iniciador de WCF transmite un `CreateSequence` del mensaje con un `Offer` elemento en una solicitud HTTP. El servicio de respuesta WCF garantiza que el `CreateSequence` tiene un `Offer` elemento, a continuación, crea una secuencia y transmite el `CreateSequenceResponse` del mensaje con un `Accept` elemento.

#### <a name="requestreply-correlation"></a>Correlación entre solicitud y respuesta

Lo siguiente se aplica a todas las solicitudes y respuestas correlacionadas:

- WCF garantiza que todos los osito de mensajes de solicitud de aplicación una `ReplyTo` referencia de punto de conexión y un `MessageId`.

- WCF aplica la referencia del extremo local como cada mensaje de solicitud de aplicación `ReplyTo`. La referencia del punto de conexión local es la `CreateSequence` del mensaje `ReplyTo` para el iniciador y la `CreateSequence` del mensaje `To` para el respondedor.

- WCF garantiza que los mensajes de solicitud entrante lleven un `MessageId` y un `ReplyTo`.

- WCF asegura la `ReplyTo` URI de la referencia de extremo de todos los mensajes de solicitud de aplicación coincide con la referencia del extremo local tal como se definió anteriormente.

- WCF garantiza que todas las respuestas llevan el valor correcto `RelatesTo` y `To` encabezados siguiendo `wsa` las reglas de correlación de solicitud/respuesta.
