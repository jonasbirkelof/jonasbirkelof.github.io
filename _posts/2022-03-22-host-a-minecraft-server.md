---
title: Host a Minecraft server
categories: [Gaming,Minecraft]
tags: [game,minecraft,server,multiplayer]
pin: false
img_path: /assets/img/
image:
    path: minecraft.jpg
---

This article will guide you in getting started with a self-hosted Minecraft server, as well as detailed configuration. you will learn how to run multiple servers at once, allowing remote players to access and open up for both Bedrock and Java users.

> IMPORTANT! Read this before continuing.
{: .prompt-warning }

> - This guide is aimed towards Windows users.
> - Your computer and server application must be running for any player to access it.
> - This guide will touch on "port forwarding" and "DNS settings" which are procedures that can be risky if you do not know what you are doing.

## 1. Installation

This guide will use the **Paper MC** server application which is fast and reliable.

1. Create a new folder and name it `mc-server` (or anything you want) anywhere on your computer.
2. Download the latest version of [Paper MC](https://papermc.io/downloads) from their website (top blue button) and save the file inside your server folder `/mc-server` that you just created.
3. Rename the file `paper.jar`.
4. Create a new text file inside `/mc-server` and paste this code:
    ```
    java -Xmx[RAM HERE] -Xms[RAM HERE] -jar paper.jar nogui
    pause
    ```
    {: file="/mc-server/start-server.bat" }
5. Change `[RAM HERE]` into the amout of RAM you want to dedicate to the server. **Be sure not to add too much!**
    2GB: 2048M, 4GB: 4096M, 8GB: 8192M

    Example:
    ```
    java -Xmx4096M -Xms4096M -jar paper.jar nogui
    pause
    ```
    {: file="/mc-server/start-server.bat" }
6. Save the file as `start-server.bat` and delete the leftover text file.
    > To make changes, rename it to `.txt`, make your changes, then rename it back to `.bat`.
    {: .prompt-tip }
7. Run `/mc-server/start-server.bat`. A couple of files will be generated in the server folder and the terminal will launch. The installation will intentionally abort after a little whileand prompt you to accept the EULA.
8. Close the terminal by typing `stop` and hit Enter.
9. Open the file `/mc-server/eula.txt` and change `eula=false` to `eula=true`. This action will accept the EULA. Save and close the file.
10. Run `/mc-server/start-server.bat` again to generate the remaining files. The terminal will say `Done` when it is finished.

The server is now running. Proceed to make some settings by following the steps below.

To stop the server, type `stop` and hit Enter.

### 1.1 Settings

There are many settings you can do, but these are the most important and common. Read more about the settings in the [Minecraft Wiki](https://minecraft.wiki/w/Server.properties).

Open `/mc-server/server.properties` and find the settings listed below. When you are done, save and close the file.

| Variabel    | Explanation                                       | Suggested value               |
| ----------- | ------------------------------------------------- | ----------------------------- |
| gamemode    | Select survival, creative, adventure or spectator | gamemode=survival             |
| difficulty  | Select peaceful, easy, normal or hard             | difficulty=normal             |
| max-players | Max simultaneous players                          | max-players=5                 |
| white-list  | Toggle whitelist                                  | white-list=true               |
| motd        | Server description                                | motd=My own Minecraft server! |

Run `/mc-server/star-server.bat` to launch the server.

### 1.2 Whitelist och admins

Det här steget är extremt viktigt eftersom vi i nästa steg kommer gå igenom hur man gör sin server tillgänglig för externa användare. Om du aktiverade whitelist i förra steget så kan du just nu inte ansluta till din server eftersom du inte står med på listan. Det ska vi fixa nu!

Se till att servern körs och att Done visas i terminalen. I terminalen skriver du kommandot whitelist add följt av ditt eget användarnamn i Minecraft, t.ex. whitelist add MyUsername och sedan Enter. Du kommer få en bekräftelse som säger Added MyUsername to the whitelist. För att ta bort användaren från listan skriver du whitelist remove MyUsername och för att visa vilka användare som är med i listan skriver du whitelist list.

Du som ägare av servern kan behöva moderera servern inifrån spelet. T.ex. kan det handla om att gå in i creative mode eller lägga till någon i whitelist. För att göra en användare (förslagsvis dig själv) till administratör (op) skriver du i terminalen op MyUsername och sedan Enter, där MyUsername är ditt användarnamn i Minecraft. Var försiktig med vilka användare du gör till administratör! För att ta bort någon som administratör skriver du deop MyUsername i terminalen och sedan Enter.

Som administratör på servern använder du samma kommandon inifrån spelet som i terminalen. För att komma åt terminalen inifrån spelet trycker du på tangenten T, skriver ”/” följt av ditt kommando, t.ex. /whitelist add my_best_friend och Enter.

Nu när du är administratör på servern och servern är låst till enbart dig och dina vänner ska vi se till att alla kan ansluta sig till den. Mer om det i nästa steg!

## 2. Anslut till servern

### 2.1 Intern anslutning

För att både du som administratör och dina vänner ska kunna ansluta till din nya server så behöver du först och främst ta reda på serverns (datorns) interna IP-nummer. Det gör du lämpligast via kommandotolken.

    Tyck på Windows + R för att öppna Kör och skriv cmd och Enter.
    I terminalen skriver du ipconfig och Enter.
    Leta reda på raden som säger IPv4 Address och notera IP-numret. Det är ditt lokala IP-nummer på ditt nätverk. Om din server finns på en annan dator i ditt lokala nätverk så måste du göra detta steg på den datorn.

Nu när du har ditt lokala IP-nummer kan du ansluta till din server. Se till att servern är igång och starta sedan Minecraft. Klicka på Multiplayer och sedan på Add server. Här kan du namnge servern vad du vill (namnet spelar ingen roll) men i fältet Adress/IP skriver du din servers IP-nummer som du just tog reda på. Klicka på Save och din server ska ligga i listan med servrar.

Du kan direkt se om du har lyckats lägga till servern. Om det av någon anledning inte gick så kommer det vara ett rött kryss på serverns rad och om det fungerade kommer du till höger se hur många användare som är inloggade.

Dubbelklicka för att ansluta till servern. Om du följt alla steg ovan så ska du nu bli placerad i en helt ny värld.

### 2.2 Skapa en ny värld

Om du inte gillar världen som har skapats så är det enkelt att generera en ny. Stoppa servern och öppna servermappen. Här raderar du mappen som heter world och även mapparna world_nether och world_end om de har skapats. Starta servern på nytt så kommer en ny värld genereras slumpmässigt.

Om du vet vilken seed du vill använda så kan du lägga till den i server.properties under variabeln level-seed innan du startar servern.

### 2.3 Extern anslutning

Tyvärr så räcker det inte att externa användare får serverns interna IP-nummer för att de ska kunna logga in eftersom det numret bara går att använda på ditt lokala nätverk. Det betyder att de måste ha ditt externa IP-nummer.

Det finns några olika sätt att ta reda på sitt externa IP-nummer men enklast är att gå till webbplatsen WhatIsMyIP.com och notera IP-numret som visas.

### 2.4 Port forward

Tyvärr så är det fortfarande inte klart… När någon besöker ditt externa IP-nummer måste nämligen din router skicka besökaren vidare till rätt ställe, nämligen din dator som kör Minecraft-servern. Det gör man genom en s.k. port forward.

Jag kommer inte gå in på exakt vad port forwarding innebär i den här guiden men man kan säga att man kopplar ihop inkommande trafik till olika platser eller funktioner på nätverket. Googla på hur du gör en port forward för just din router och följa anvisningarna.

    Skapa en ny anslutning och ge den ett namn, t.ex. Minecraft Server
    Ange eller välj din dators lokala IP-nummer
    Ange porten för din Minecraft-server (25565)

Din Minecraft-server ligger som standard på port 25565 och din port forward gör så att när någon extern användare försöker ansluta till ditt externa IP-nummer via Minecraft så kommer den skickas till port 25565 vilket är din Minecraft-server.

Det enda dina vänner behöver göra nu är att lägga till din server med ditt externa IP-nummer, precis som du själv gjorde ovan (fast du använde ditt lokala IP-nummer) och ansluta till din värld!

Glöm inte bort att lägga till dina vänner i whitelist!

Grattis! Du har nu installera en helt egen Minecraft-server som du kan spela på tillsammans med dina vänner. Om både du och dina vänner spelar på Java-versionen av Minecraft så är det bara att köra, men om någon behöver ansluta via en Bedrock-version så kommer inte det gå eftersom de olika versionerna hanterar UUID (Unique User ID) olika. Gå vidare till nästa steg för att gå runt det problemet eller fortsätt läsa om DNS-inställningar, vilket är valbart men kan vara trevligt att göra.

## 3. Gör servern tillgänglig för Bedrock-användare

För att Bedrock-användare ska kunna ansluta till din Java-server behöver du installera en plugin som heter Geyser på din server. Du behöver dessutom installera Floodgate för att Bedrock-användarna ska slippa köpa ett Java-konto för att ansluta sig.

    Ladda ner Geyser via hemsidan och gå till Download. Ladda ner filen Geyser-Spigot.jar.
    Ladda ner Floodgate via hemsidan och ladda ner filen floodgate-spigot.jar.

    Stoppa servern om den är igång genom att skriva stop i terminalen och sedan Enter.
    Lägg filen Geyser-Spigot.jar i mappen plugins i servermappen men kör den inte.

För att följande steg ska fungera får ingen annan server köras under tiden!

    Starta servern med start_server.bat. Nu ska en Geyser-mapp med filer skapas i plugins-mappen.
    Stoppa servern genom att skriva stop i terminalen och sedan Enter.
    Lägg filen floodgate-spigot.jar i mappen plugins men kör den inte.
    Starta servern på nytt. Nu ska en Floodgate-mapp med filer skapas i plugins-mappen.
    Öppna Floodgate-mappen och kopiera filen key.pem och klistra in den i Geyser-mappen.

Nu måste du göra en ny port forward på samma sätt du du gjorde i avsnittet ovan, men istället för att peka till port 25565 så ska du peka till port 19132, vilket är den port som Berock-versionen använder som standard. När detta är gjort kan både Java- och Bedrock-användare logga in på servern med det externa IP-numret. Bedrock-användare ansluter via port 19132 och Java-användare 25565 om det efterfrågas.

    Tips!

    Om det inte går att lägga till servern i Minecraft via enbart IP-numret, prova att lägga till portnumret efter på det här viset: 123.456.789:19132 där 123.456.789 är ditt externa IP-nummer.

### 3.1 Whitelist för Bedrock-användare

Nu måste du lägga till Bedrock-användarna i whitelist men eftersom de har en annan sorts UUID än Java-användarna så går det inte att göra som vanligt. Följ stegen nedan för att lösa det!

Se till att följande steg är utförda enligt instruktionerna ovan:

    Whiltelist är aktiverat
    Du ligger med i whiltelist
    Du är administratör (op) på servern

Fortsätt sedan med följande steg:

    Stoppa servern genom att skriva stop i terminalen och sedan Enter.
    Inaktivera whitelist genom att ändra white-list=true till white-list=false.
    Nu ska både du och Bedrock-användaren logga in på servern.
    Observera att Bedrock-användarens användarnamn har en punkt (.) framför sig. Det är för att skilja på olika användarnamn eftersom båda användarnamnen kan existera i de olika versionerna av spelet, eftersom de har olika typer av UUID.
    När ni båda är inne i spelet öppnar du meddelandefältet T och skriver /whitelist add .[Bedrock-användarens användarnamn], t.ex. /whitelist add .MyBedrockFriend. Observera punkten före användarnamnet.
    Nu loggar ni båda ut från spelet.
    Stoppa servern och aktivera whitelist igen genom att ändra white-list=false till white-list=true i server.properties.

Att lägga till spelaren via terminalen i servern fungerar inte eftersom vi inte vet Bedrock-användarens UUID förrän denne är inloggad på srevern. När whitelist är inaktiverat och spelaren är inne i spelet har Floodgate givit anvädaren ett nytt användarnamn (med en punkt framför) och dennes UUID kan då användas till whitelist.

Du kan kontrollera att Bedrock-användaren har lagts till samt dennes UUID genom att öppna filen whitelist.json. Notera att Bedrock-användarens UUID ser annorlunda ut än Java-användarnas.

    Tips!

    När en Bedrock-användare har lagts till i whitelist enligt ovan så kan man kopiera posten i whitelist.json och klistra in den i andra servrars whitelist.json (mer om det nedan). Man behöver alltså bara göra detta en gång per användare!

## 4. Gör DNS-inställningar

Om du vill och har möjlighet så kan du peka en domän via DNS till ditt externa IP-nummer så att du och besökarna ansluter till servern med domänen, t.e.x mcserver.minsida.se istället för IP-numret. Detta kräver att du äger en domän och att din host tillåter dig att göra DNS-inställningar. Detta går bra med t.ex. One.com.

    Tips!

    Använd länken nedan för att få 120 kr rabatt
    på ditt första köp hos One.com!

    http://one.me/svayjtwm

Såhär gör du för att ställa in domän att peka till din Minecraft-server:

    Logga in på ditt webbhotell/DNS-host och gå till sidan för DNS-inställningar.
    Skapa en A-post (adress till IP) med följande inställningar:
        Värdnamn: välj en subdomän, t.ex. mcserver, så att värdnamnet blir mcserver.minsida.se.
        Peka till IP: ange det externa IP-numret som adressen ska peka till.

    Skapa en SRV-post (adress till port) med följande inställingar:
        Värdnamn: Måste ha en speciell form: _[beskrivning]._tcp.[subdomän].[toppdomän], t.ex. _minecraft._tcp.mcserver.minserver.se
        Peka till: Även denna måste vara på en speciell form: [vikt] [port] [mål], t.ex. 5 25565 mcserver.minsida.se.

Det kan ta lite tid innan DNS-inställningarna går igenom. Detta beror på din DNS-host. Minaerfarenheter är att One.com hanterar detta så gott som omedelbart och är igån inom ett par minuter. När inställningarna har gåt igenom så ska du nu kunna ansluta till din Minecraft-server med den andress du angav, t.ex. mcserver.minsida.se istället för ditt externa IP-nummer och port.

## 5. Kör flera servrar (och världar) på samma dator samtidigt

En Minecraft-server kan bara innehålla en värld åt gången. För att kunna ha flera världar igång samtidigt måste man köra flera servrar samtidigt. Man åstakommer detta genom att göra allt som vi gjort i steg 1-2 (och övriga steg om det behövs) för varje server som ska vara igång.

    Skapa en mapp för varje server och följ installationsprocessen i steg 1 och 2 ovan. Följ även stegen för Geyser och Floodgate om det behövs.
    Ändra server-port i server.properties för alla servrar. Den första servern kan ha default port (25565) men de andra servrarna måste använda andra portar, t.ex. 25566, 25567, osv. Du gör iställningen under server-port=25565.
    Om du använder Geyser och Floodgate så måste du ändra port för Java och Bedrock i filen config.yml som ligger i mappen plugins/Geyser-Spigot/ till samma port som du sätter i server.properties. Porten för Bedrock ligger ganska högt upp i filen och porten för Java längre ner.
    Gör en ny port forward, men för de nya portarna för de nya servrarna. Glöm inte bort portarna för Bedrock.