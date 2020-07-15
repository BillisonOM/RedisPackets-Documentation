# RedisPackets-Documentation
RedisPackets library documentation

### How to initialize
```java
  private void loadRedis(){
    RedisHandler handler = new RedisHandler(channel, address, port, password);
    handler.registerListener(listener);
    handler.registerPacket(new ExamplePacket());
    handler.sendPacket(new ExamplePacket("test"));
  }
```

### Packet Example
```java
package org.jefferies.packets.example;

import com.google.gson.JsonObject;
import lombok.AllArgsConstructor;
import lombok.NoArgsConstructor;
import org.jefferies.packets.RedisPacket;

@AllArgsConstructor
@NoArgsConstructor
public class ExamplePacket extends RedisPacket {

    private String message;

    @Override
    public String getIdentifier() {
        return "ExamplePacket";
    }

    @Override
    public JsonObject serialized() {
        JsonObject object = new JsonObject();
        object.addProperty("message", message);
        return object;
    }

}
```

### Packet Listener Example
```java
package org.jefferies.packets.example;

import com.google.gson.JsonObject;
import org.jefferies.packets.listener.PacketListener;
import org.jefferies.packets.listener.RedisListener;

public class Listener extends RedisListener {

    @PacketListener(identifier = "ExamplePacket")
    public void onExecute(JsonObject object){
        String message = object.get("message").getAsString();
        System.out.println(message);
    }

}
```

### Example Result
https://prnt.sc/t29n0d
