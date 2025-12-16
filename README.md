# Xinyu Edu and Rsch Network | AS151673

The bird2 config for Xinyu Edu and Rsch Network
Forked and developed From [MoeQing](https://github.com/MoeQing-Network/MoeQing-Network-BIRD2-Config)

Add the function of Action to node
Add the function of default catch_all for downstreams
Add the function of special route announce control
This network is a via 6, so Add IPv4 support

## Internal Community:

>(151673, <999,  0)            Community for all my node
>
>(151673, <999,  1)            Community only for this node

```
(151673,   1, *)   do not send to ibgp
(151673,   2, *)   do not send to ebgp
(151673,   3, *)   do not send to kernel
(151673,   4, *)   send to kernel but mark unreachable
(151673,   5, *)   send to kernel but mark blackhole
(151673, 101, *)   allow bgp_local_perf
(151673, 201, *)   transit routes
(151673, 202, *)   ixp rs routes
(151673, 203, *)   peer routes
(151673, 204, *)   customer routes
(151673, 209, *)   ibgp routes
(151673, 210, 0)   Special routes type 1
(151673, 211, 0)   Special routes type 2
(151673, 212, 0)   Special routes type 3
(151673, 213, 0)   Special routes type 4
(151673, 214, 0)   Special routes type 5
```

## Control Community:
```
 Actions:
  * = 0   do not announce to target
  * = 1   prepend 1 to target
  * = 2   prepend 2 to target
  * = 4   prepend 4 to target
  * = 8   prepend 8 to target
 Action target selector:
  * = Action
  (151673, 1*00, 0)            Do action to everyone
  (151673, 1*01, asn)          Don't do action to this asn
  (151673, 1*02, asn)          Do action to this asn
  (151673, 1*10, 0)            Do action to every region
  (151673, 1*11, region_code)  Don't do action to this region
  (151673, 1*12, region_code)  Do action to this region
  (151673, 1*13, node_code)    Don't do action to this node
  (151673, 1*14, node_code)    Do action to this node
  (151673, 1*15, special_route_type) Do action to route with special route type code 210-214 with should effective in where should export route to others, before the fliter.
  (151673, 1019, 0)            Disable (asn, 1010, 0),  (asn, 1011, local_region) as default value
  (151673, 1*20, 0)            Do action to every country
  (151673, 1*21, country_code) Don't do action to this country
  (151673, 1*22, country_code) Do action to this country
  (151673, 1*30, 1)            Do action to upstreams
  (151673, 1*30, 2)            Do action to ixp rs
  (151673, 1*30, 3)            Do action to peers
  (151673, 1*30, 4)            Do action to downstreams
  (151673, 1*30, 8)            Do action to route collectors
```

## Examples:
```
  prepend 11 to AS6939: 
     (151673, 1102, 6939): prepend 1 to AS6939
     (151673, 1202, 6939): prepend 2 to AS6939
     (151673, 1802, 6939): prepend 8 to AS6939
                 Total : 1+2+8 = 11
  prepend 2 to everyone but 6939:
    (151673, 1200, 0):     prepend 2 to everyone
    (151673, 1201, 6939):  don't do this action(prepend 2) to AS6939
  do not announce to anyone: 
    (151673, 1000, 0):     do not announce to everyone
  announce to all region:
    (151673, 1019, 0):     announce to all region
  announce in Asia-E only:
    (151673, 1010, 0):     do not announce to every region
    (151673, 1011, 52):    but announce to Asia-E region
```

## Informational Community
```
(151673, 10000, region_code)    Received from region
(151673, 10001, country_code)   Received from country
```

## Region code:
```
* 41: Europe
* 42: North America-East
* 43: North America-Central
* 44: North America-West
* 45: Central America
* 46: South America-Central
* 47: South America-West
* 48: Africa-N (above Sahara)
* 49: Africa-S (below Sahara)
* 50: Asia-S (IN, PK, BD)
* 51: Asia-SE (TH, SG, PH, ID, MY)
* 52: Asia-E (JP, KR, TW, HK, CN)
* 53: Pacific&Oceania (AU, NZ, FJ)
* 54: Antarctica
* 55: Asia-N (RU)
* 56: Asia-W (IR, TR, UAE)
* 57: Central Asia (AF, UZ, KZ)
```

## Country code:
ISO-3166 numeric-3 country code

## Credits

* Special thanks [KusakabeShi](https://github.com/KusakabeShi)
* [Soha Jin](https://github.com/moesoha)
* Razuritta