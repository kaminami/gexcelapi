GExcelAPI
=========

- https://github.com/nobeans/gexcelapi がオリジナル
- bintrayのサービス終了に伴い、https://github.com/kaminami/gexcelparser から利用するためにフォークしたリポジトリ


GExcelAPI is a thin Groovy-ish wrapper library of not JExcelAPI but Apache POI.




Getting Started
---------------

It's difficult to read and write when using Apache POI directly.
Especially, an identification of a cell to use an index is too complicated and ugly.

```groovy
File inputFile = ...
def book = new HSSFWorkbook(new POIFSFileSystem(new FileInputStream(inputFile)))
def sheet = book.getSheetAt(0) // 1st sheet
println "A1: " + sheet.getRow(0)?.getCell((short) 0)
println "A2: " + sheet.getRow(1)?.getCell((short) 0)
println "B1: " + sheet.getRow(0)?.getCell((short) 1)
```

By using GExcelAPI, you can write the above sample like this:

```groovy
File inputFile = ...
def book = GExcel.open(inputFile)
def sheet = book[0] // 1st sheet
println "A1: " + sheet.A1.value
println "A2: " + sheet.A2.value
println "B1: " + sheet.B1.value
```

---------------------
build.gradle

```
apply plugin: "groovy"

repositories {
    mavenCentral()

    // gexcelapi
    maven {
        url 'https://github.com/kaminami/gexcelapi/raw/master/repository'
    }
}

dependencies {
    compile group: 'org.codehaus.groovy', name: 'groovy-all', version: '2.4.21'
    compile group: 'org.apache.poi', name: 'poi-ooxml', version: '3.10.1'
    compile 'kaminami:gexcelapi:0.4.1'
}
```

License
-------

GExcelAPI is released under the [Apache 2.0 License](http://www.apache.org/licenses/LICENSE-2.0)
