# Basics

# Was ist ein Turti-Programm?

- Ein Turti-Programm wird dauerhaft auf einer Turtle installiert und bei jedem start automatisch ausgeführt.
- Stürtzt die Turtle ab (durch z.B. Server-Neustart / Fahren in einen nicht geladenen Junk), wird das Programm beim
  Neustart **fortgeführt** und beginnt **nicht** von neuem.
- Turti-Programme werden in der Sprache [Turti](#Turti) geschrieben

# Installation eines Turti-Programms

Beispiel installations-Command für das Programm [Holla](#holla):
> pastebin run FauBfvYe svdv6kJJ

- FauBfvYe: Turti-Installer, bleibt immer gleich
- svdv6kJJ Holla-Programm auf pastebin (für neues Programm einfach anpassen)

Wichtig: Das Programm muss nur **einmal installieren** und wird dann **bei jedem Neustart** von pastebin heruntergeladen
und **ausgeführt**

Um ein Programm von neuem zu Starten kann folgender Befehl verwendet werden:
> turti restart

# Turti

## Holla

Das Holla-Programmbeispiel fungiert als Hello-World Programm.

<pre><code>main: {
    print("Holla!")
}</code></pre>

## Syntax

<pre><code>
// Kommentar mit '//'
/*
    Block-Kommentar mit '/**/'
*/

// Jedes Programm in Turti besteht aus mindestens einem Funktions-Block, der den Hauptcode enthält:
main: {
    // Variablendeklaration:
    i = 1;
    b = true;
    s = "huihuihui";
    
    // if
    if (x < 5) {
        ...    
    }; //  (Semikolon nach jedem Statement!)

    // if else
    if (x < 5) {
        ...    
    } else if (x < 7) {
        ...
    } else {
        ...
    };

    // while
    while (true) {
        ...    
    };
    
    // for
    for (x=0; x<5; x++) {
        ...
    };

    // Boolesche Operationen
    x = y && true || a; // && wird immer zuerst ausgeführt
    x = y && (true || a); // Um || zuerst auszuführen sind Klammern nötig

    // Arithmetische Operationen
    x = y + 2 - 3;
    x++;
    x--;
    ++x;
    ++y;

    // Vergleiche
    x = y >= 3;
    x = y <= 3;
    x = y == 3;
    x = y > 3;
    x = y < 3;
    x = y != 3;

    // Arrays
    x = [1, null, 2, true, "ha"];
    x[2]; // 2
    x[2] = 3; // x: [1, null, 3, true, "ha"]

    // Länge über .length
    for(i = 0; i < arr.length; i++){
        print(arr[i]);
    };

    // error (index out of bounds)
    arr[-1];
    arr[5];

    // Globale Konstanten (verfügbar in allen Funktionen)
    $TYPE$ = "hui";
    x = $TYPE$;

    // Funktionsaufruf
    echo(1, 2, 3);
}; // Semikolon auch nach Funktionen

// Funktion
echo(x,y,z): {
    print(x + ", " + y + ", " + z);
};

// wird vor 'main' ausgeführt, initialisiert Konstanten
init: {
    $ID_COMPUTER$ = "...";
}</code></pre>

## Standard-Bibliothek

Optionale argumente sind mit [] gekennzeichnet
<pre><code>main: {
    // Print 
    print("hu");

    // Bewegung (Blöcke und Entities auf dem Weg werden entfernt)
    mvFwd([x:int]);
    mvBack([x:int]);
    mvUp([x:int]);
    mvDown([x:int]);
    left([x:int]);
    right([x:int]);
    
    // Blöcke abbauen / platzieren
    dig([slot:int], [item:string]); // item gibt das erwartete item an (wenn angegeben stellt die Turtle sicher, dass der Slot nur items dieses Typs enthält)
    digUp([slot:int], [item:string]);
    digDown([slot:int,] [item:string]);
    place(slot:int);
    placeUp(slot:int);
    placeDown(slot:int);

    // Inventar-Zugriff
    getItemName(slot:int);
    getItemCount(slot:int);
    drop(slot:int, [count:int]); // count ist 1 per default
    dropUp(slot:int, [count:int]);
    dropDown(slot:int, [count:int]);
    suck([slot:int], [count:int]);
    suckUp([slot:int], [count:int]);
    suckDown([slot:int], [count:int]);
    equipRight([slot:int]);
    equipLeft([slot:int]);

    // delay
    sleep(seconds:int);

    // fuel
    getFuelLevel();
    refuel();

    // shell
    shell("pastebin","get","...");
    
    // user-input
    x = input("text:");
    
    // Konvertierung von text in Zahl
    tonumber(x);

    // splitten eines Texts
    x = splitText("1,2,3", ","); // Ergebnis ist ["1","2","3"]
    a, b, c = x; // Auflösen des Arrays
}</code></pre>

# Turti-Bibliotheken

Turti-Bibliotheken erweitern die Sprache um eine Menge an Funktionen.
Zum Beispiel fügt die *smartGPS*-Bibliothek (iT4NKZfx) die Funktion *moveTo(...)* hinzu.

## Smart GPS

Die smartGPS-Bibliothek ermöglicht das navigieren zu einer Position mithilfe des A* Algorithmus.
Die Turtle merkt sich dabei auch ein Stück weit ihre Umgebung.

<pre><code>#import: iT4NKZfx; // importieren der GPS-Bibliothek

main: {
    // an eine Position bewegen (benötigt import der GPS-Bibliothek)
    moveTo([x:int,y:int,z:int], direction:int); // direction ist die Richtung, in die die Turtle sich ausrichten soll

    // einen Block ansehen (von einer beliebigen Seite)
    faceToward([x:int,y:int,z:int]);

    // einen Block der Liste ansehen (von einer beliebigen Seite)
    // Gibt den Index des angesehenen Blocks zurück (0..n-1)
    faceTowardAny([x1:int,y1:int,z1:int], [x2,y2,z2], ...);

    // Position ermitteln
    locate();
  
    // Ausrichtung ermitteln
    getDirection();

    // Ausrichtung setzen (die turtle dreht sich entsprechend)
    setDirection(0);

    // Position eines Blocks in bestimmter Richtung
    getPosInDirection([0,0,0],0); // gibt [1,0,0] zurück
  
    // direction=0 -> positive x-Richtung (1. Minecraft-Koordinate)
    // direction=1 -> positive z-Richtung (3. Minecraft-Koordinate)
    // direction=2 -> negative x-Richtung (1. Minecraft-Koordinate)
    // direction=3 -> negative z-Richtung (3. Minecraft-Koordinate)
    // direction=4 -> positive y-Richtung (2. Minecraft-Koordinate)
    // direction=5 -> negative y-Richtung (2. Minecraft-Koordinate)
}

</code></pre>

## Toggle Item

Die toggleItem-Bibliothek wechselt je nach Bedarf Spitzhacke und Ender Modem.

<pre><code>#import: mWBVHmn0;

main: {
  // den letzten Slot für Item-Switching definieren (muss eines der Items enthalten, das andere muss ausgerüstet sein)
  configureItemSwitch(15, "left");
  // optional können item-ids übergeben werden:
  configureItemSwitch(15, "left", );

  // Modem wird für gps-Befehle ausgerüstet
  locate();

  // Spitzhacke wird für dig-Befehle ausgerüstet
  dig();
  
}

</code></pre>

## Math

<pre><code>#import: AAMw1hB3;

main: {
    min(1, 2, 3, 4);
    max(5, 6);
    x, y = minMax(2, 6, 5, 3); // -> gibt [2, 6] zurück

    abs(x);
}

</code></pre>

## Definition von Bibliotheken

Die folgende Bibliothek definiert eine Funktion *test()*, die den übergebenen wert auf der Konsole ausgibt:

```lua
local api = {}

function api.test(value)
    print(value)
end

return {
    name = "testBibliothek", -- name der Bibliothek
    api = api -- Funktions-Definition
}
```

Benutzt werden kann die Bibliothek folgendermaßen:
<pre><code>#import: iT4NKZfx; // Bibliothek auf Pastebin

main:{
  test("Hu")
}
</code></pre>
Zugehörige Ausgabe auf der Konsole: <code>Hu</code>

## Speichern von Daten in Bibliotheken

Daten, die außerhalb von Funktionen verwendet werden, dürfen in Turti-Bibliotheken *nicht* in globalen variablen
gespeichert werden.

Stattdessen wird ein *storage*-Objekt verwendet:

```lua
local api = {}
local storage
local save

function api.setValue(value)
    storage.value = value
    save() -- Speichern der Daten des Storage (sollte nach Änderungen aufgerufen werden)
end

function api.getValue(value)
    return storage.value
end

return {
    name = "testBibliothek", -- name der Bibliothek
    api = api, -- Funktions-Definition
    onInitStorage = function(_storage, _save)
        -- Initialisieren des Storage
        storage = _storage
        save = _save
    end
}
```

Die Daten bleiben während der Ausführung des Programms im Storage erhalten, auch wenn der Computer oder das Programm
abstürzen sollte. Allerdings werden die Daten gelöscht, wenn das Programm erfolgreich endet.

## Speichern von Daten über mehrere Ausführungen des Programms hinaus

Der *persistentStorage* speichert Daten permanent auf dem Computer / der Turtle und wird wie der normale Bibliotheks-
*storage* verwendet:

```lua
local api = {}
local storage
local save
local persistentStorage
local persistentSave

-- Wert innerhalb der Laufzeit speichern
function api.setValue(value)
    storage.value = value
    save()
end

function api.getValue(value)
    return storage.value
end

-- Wert permanent speichern
function api.setValuePersistent(value)
    persistentStorage.value = value
    persistentSave()
end

function api.getValuePersistent(value)
    return persistentStorage.value
end

return {
    name = "testBibliothek", -- name der Bibliothek
    api = api, -- Funktions-Definition
    onInitStorage = function(_storage, _save)
        -- Initialisieren des Storage
        storage = _storage
        save = _save
    end,
    onInitPersistentStorage = function(_pStorage, _pSave)
        -- Initialisieren des persistent Storage
        persistentStorage = _pStorage
        persistentSave = _pSave
    end
}
```

Natürlich muss nicht zum Speichern jedes Werts eine Funktion angelegt werden, die Daten der *storages* können beliebig
oft verändert werden. Nur sollte nach den Änderungen ein *save()* - / *persistentSave()* - Aufruf folgen.
