# diag filter for Asciidoc #

Takeshi Komiya has created a suite of diagram layout toolst:  http://blockdiag.com/en/index.html

Using the asciidoc-diag filter, diagrams created by any of these programs  can be embedded into Asciidoc documents and processed into either PNG bitmap or SVG vector graphics.


## Prerequisites ##

install the seqdiag, blockdiag, nwdiag, packetdiag, actdiag programs as
outlined here: http://blockdiag.com/en/index.html, for instance like so:

> `sudo easy_install blockdiag seqdiag actdiag nwdiag packetdiag`

## Versions ##

There are two versions:

  * diag-filter.conf: for newer asciidoc versions. will create PNG's for HTML and use SVG diag output for PDF.

  * diag-filter-old.conf: needed for older asciidoc versions, eg asciidoc 8.5.2 which comes with Ubuntu 10.04 LTS. This version cannot handle certain macros (counter2) and therefore this is PNG only also for PDF's. Also, older versions of asciidoc cannot default the 'target="image-basename"' positional attribute so it must be given as in below examples.

## Examples ##
The examples below are taken from the  seqdiag/blockdiag/nwdiag/packetdiag/actdiag distributions.

creating pdf:: a2x  -f pdf --asciidoc-opts "-f diag-filter-old.conf" diag-test-old.txt

creating html:: asciidoc -f diag-filter-old.conf diag-test-old.txt


replace by the  diag-filter-old.conf and diag-test-old.txt by
diag-filter.conf and diag-test.txt for newer asciidoc versions.

```
["seqdiag",target="seqdiag-1.png"]
---------------------------------------------------------------------
{
  // edge label
  A -> B [label = "call"];
  A <- B [label = "return"];

  // diagonal edge
  A -> B [diagonal, label = "diagonal edge"];
  A <- B [diagonal, label = "return diagonal edge"];
}
---------------------------------------------------------------------
```

![https://asciidoc-diag-filter.googlecode.com/git/seqdiag-1.png](https://asciidoc-diag-filter.googlecode.com/git/seqdiag-1.png)

```
["seqdiag",target="seqdiag-2.png"]
---------------------------------------------------------------------
{
  // normal edge
  A -> B [label = "normal edge"];

  // dotted edge
  B --> C [label = "dotted edge"];

  // asynchronus edge
  A ->> B [label = "asynchronus edge"];
  B -->> C [label = "asynchronus dotted edge"];

  // return edge
  B <- C [label = "return edge"];
  A <-- B [label = "return dotted edge"];
  B <<- C [label = "return asynchronus edge"];
  A <<-- B [label = "return asynchronus dotted edge"];

  // self referenced edge
  A -> A [label = "self referenced edge"];
}
---------------------------------------------------------------------
```

![https://asciidoc-diag-filter.googlecode.com/git/seqdiag-2.png](https://asciidoc-diag-filter.googlecode.com/git/seqdiag-2.png)

```
["blockdiag",target="blockdiag-1.png"]
---------------------------------------------------------------------
blockdiag {
   A -> B -> C -> D;
   A -> E -> F -> G;
}
---------------------------------------------------------------------
```

![https://asciidoc-diag-filter.googlecode.com/git/blockdiag-1.png](https://asciidoc-diag-filter.googlecode.com/git/blockdiag-1.png)

```
["packetdiag",target="packetdiag-1.png"]
---------------------------------------------------------------------
diagram {
  colwidth = 32
  node_height = 72

  0-15: Source Port
  16-31: Destination Port
  32-63: Sequence Number
  64-95: Acknowledgment Number
  96-99: Data Offset
  100-105: Reserved
  106: URG [rotate = 270]
  107: ACK [rotate = 270]
  108: PSH [rotate = 270]
  109: RST [rotate = 270]
  110: SYN [rotate = 270]
  111: FIN [rotate = 270]
  112-127: Window
  128-143: Checksum
  144-159: Urgent Pointer
  160-191: (Options and Padding)
  192-223: data [colheight = 3]
}
---------------------------------------------------------------------
```
![https://asciidoc-diag-filter.googlecode.com/git/packetdiag-1.png](https://asciidoc-diag-filter.googlecode.com/git/packetdiag-1.png)
```
["nwdiag",target="nwdiag-1.png"]
---------------------------------------------------------------------
diagram {
  network dmz {
      address = "210.x.x.x/24"

      web01 [address = "210.x.x.1"];
      web02 [address = "210.x.x.2"];
  }
  network internal {
      address = "172.x.x.x/24";

      web01 [address = "172.x.x.1"];
      web02 [address = "172.x.x.2"];
      db01;
      db02;
  }
}
---------------------------------------------------------------------
```

![https://asciidoc-diag-filter.googlecode.com/git/nwdiag-1.png](https://asciidoc-diag-filter.googlecode.com/git/nwdiag-1.png)
```
["actdiag",target="actdiag-1.png"]
---------------------------------------------------------------------
actdiag {
  write -> convert -> image

  lane user {
     label = "User"
     write [label = "Writing reST"];
     image [label = "Get diagram IMAGE"];
  }
  lane actdiag {
     convert [label = "Convert reST to Image"];
  }
}
---------------------------------------------------------------------
```

![https://asciidoc-diag-filter.googlecode.com/git/actdiag-1.png](https://asciidoc-diag-filter.googlecode.com/git/actdiag-1.png)