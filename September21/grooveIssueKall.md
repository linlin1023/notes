# Illegal reflective access by org.codehaus.groovy.reflection.CachedClass


Tue Oct 12 10:41:02 NZDT 2021:Group-4:err:WARNING: Illegal reflective access by org.codehaus.groovy.reflection.CachedClass$3$1 (file:/qa/src/javaservices/java00/java/sites/java00/9.60.1069/dist/groovy-all-1.6.7.jar) to method java.lang.Object.finalize()
Tue Oct 12 10:41:02 NZDT 2021:Group-4:err:WARNING: Please consider reporting this to the maintainers of org.codehaus.groovy.reflection.CachedClass$3$1
Tue Oct 12 10:41:02 NZDT 2021:Group-4:err:WARNING: Use --illegal-access=warn to enable warnings of further illegal reflective access operations


MR: https://github.com/apache/groovy/pull/811/

$ env | grep GROOVY
GROOVY_TURN_OFF_JAVA_WARNINGS=true

# set up two test environments to compare the code change impacts
1. chbase --> map code
2. base --> check if you change the map code
3. setupsql mysql
4. chjbase 9.60.1 11  --> change java code version and java version
5. jbase ---> change java code version
6. restinit -a --->restore all,any change happened to map just done by change link to the code base, but the java you need run some command
7. restsjava csc_randwhit  ---> dataset and install the site
8. Copy groovy script file for Xmgen VUE corrugator protocol configuration and paste it to xmgen config directory.
9. cp $JCSC/files/marquip_test_realtime.config.script $JCSC/conf/kiwiplan/xmgen/config/

$JCSC is the installdir $INSTALLDIR

groove upgrade from 2.5 to 3.0, the jar is change to pom, the split the implementation code into separate jars

# run remote deploy script to deploy new built jar to remote 

mount the remote dir
 sshfs -p 22 -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no -o workaround=rename -o follow_symlinks java00@nzscxmit1:/qa/KIWI ~/base


 deploy --nojar -v --base ~/base --tomcat ~/base/services/web/java00/current java00

 deploy --nojar -v --base ~/base java00

have a try in my local 
 deploy --nojar -v --base /KIWI --tomcat /kiwi/services/web/valley2/current valley2

current installed directory is /javaservice/java00/java/sites/java00/current,   but our base is mount to /qa/KIWI
create a softlink "services" inside "/qa/KIWI" point to  "/javaservice/java00/java", so we get the path like /qa/KIWI/services/sites/java00/current. so the path "/qa/KIWI" can be treated as the base directory.

sitename java00 in this case

 vue : /qa/KIWI/services/4266
 tomcat: /qa/KIWI/services/web/4266

 grep -irl "foo" 2> /dev/null

find / -name groovy-all-3.0.9.pom 2>&1 | grep -v "Permission denied"


cksum *.jar


find / -name groovy*3.0.9.jar 2>&1 | grep -v "Permission denied"
find / -name groovy-all-3.0.9.pom 2>&1 | grep -v "Permission denied"

# new feature of groovy 3.0, (2.5 not support below features)

## Parrot parser
 ### Java's class do/while loop supported now
 ```groovy
 def count = 5
 def fact = 1
 do {
         fact *= count--
 } while (count > 1)
 assert fact == 120
 ```

 ### Multi-assignment in combination with for loop

 ```groovy
 def (String x, int y) = ['foo', 42]
 assert "$x $y" == 'foo 42'
 ```

 ```groovy
 deg baNums = []
 for (def (String u, int v) = ['bar', 42]; v < 45; u++, v++) {
         baNums << "$u $v"
 }

 assert baNums == ['bar 42', 'bas 43', 'bat 44']
 ```

### java-style array in initialization

```groovy
def pets = new String[] {'cat', 'dog'}
assert pets.size() == 2 && pets.sum() == 'catdog'
assert pets.class.name == '[Ljava.lang.String;'
```

### java style lambda syntax

```groovy
 (1..10).forEach(e -> {println e})

  assert (1..10).stream()
  .filter(e->e%2==0)
  .map(e->e*2)
  .toList() == [4,8,12,16,20]
```
### method reference

```groovy
  assert ['1','2','3'] == 
        Stream.of(1,2,3)
        .map(String::valueOf).toList()

```

### !instanceof !in  syntax sugar
```groovy
  
  assert 45 !instanceof Date
  
  assert 45 !in [1,2,3,5]

```

### Elvis assignment operator  (some kind of syntax sugar)

```groovy

@ToStrnig
class Element {
        String name
        int atomicNumber
}

def he = new Element(name: 'Helium')
he.with {
        name = name ? : 'Hydrogen'
        atomicNumber ?= 2
}
assert he.toString() == 'Element(Helium, 2)'

```

### identity comparison

===  !==   .is()

```groovy

@EqualsAndHashCode
class Creature { String type }

def cat = new Creature(type: 'cat')
def lion = new Creature(type: 'cat')
def copyCat = cat 

assert cat.equals(lion)
assert cat == lion

assert cat.is(copyCat)
assert cat === copyCat
assert lion !== cat

```

### Safe indexing

```groovy
String[] array = ['a', 'b']
assert 'b' == array?[1]
array?[1] = 'c'
assert 'c' == array?[1]

array = null
assert null == array?[1]  // return null for all index values
array?[1] = 'c' // quietly ignore attempt to set value
assert null == array?[1]

//map index
def personInfo = [name: 'Daniel.Sun', location: 'Shanghai']
assert 'Daniel.Sun' == personInfo?['name']
personInfo?['name'] == 'sunlan'
assert 'sunlan' == personInfo?['name']
 
personInfo = null
assert null == personInfo?['name']
personInfo?['name'] = 'sunlan'
assert null == personInfo?['name']
```

### nested code blocks


