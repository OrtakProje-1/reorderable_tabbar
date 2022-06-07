## Setup

```yaml

    dependencies:
        reorderable_tabbar:
            git: https://github.com/OrtakProje-1/reorderable_tabbar.git
    
```


## Example

```dart

    

class ReorderableTabBarPage extends StatefulWidget {
  ReorderableTabBarPage({Key? key}) : super(key: key);

  @override
  State<ReorderableTabBarPage> createState() => _ReorderableTabBarPageState();
}

extension StringExt on String {
  Text get text => Text(this);
  Widget get tab {
    return Tab(
      text: this,
    );
  }
}

class _ReorderableTabBarPageState extends State<ReorderableTabBarPage> {
  PageController pageController = PageController();

  int index = 9;

  List<String> tabs = [
    "1",
    "2",
    "3",
    "4",
    "5",
    "6",
    "7",
    "8",
  ];

  bool isScrollable = false;
  bool tabSizeIsLabel = false;

  @override
  Widget build(BuildContext context) {
    return DefaultTabController(
      length: tabs.length,
      child: Scaffold(
        appBar: AppBar(
          elevation: 0,
          title: Text("Reorderable TabBar"),
          actions: [
            Padding(
              padding: const EdgeInsets.all(8.0),
              child: Center(
                child: Switch(
                  activeColor: Colors.white,
                  inactiveThumbColor: Colors.grey.shade400,
                  value: tabSizeIsLabel,
                  onChanged: (s) {
                    setState(() {
                      tabSizeIsLabel = s;
                    });
                  },
                ),
              ),
            ),
            Padding(
              padding: const EdgeInsets.all(8.0),
              child: Center(
                child: Switch(
                  activeColor: Colors.white,
                  inactiveThumbColor: Colors.grey.shade400,
                  value: isScrollable,
                  onChanged: (s) {
                    setState(() {
                      isScrollable = s;
                    });
                  },
                ),
              ),
            ),
          ],
          bottom: ReorderableTabBar(
            tabs: tabs.map((e) => e.tab).toList(),
            indicatorSize: tabSizeIsLabel ? TabBarIndicatorSize.label : null,
            isScrollable: isScrollable,
            indicatorColor: Colors.blueGrey.shade900,
            reorderingTabBackgroundColor: Colors.black45,
            indicatorWeight: 5,
            tabBorderRadius: BorderRadius.vertical(
              top: Radius.circular(8),
            ),
            onReorder: (oldIndex, newIndex) async {
              String temp = tabs.removeAt(oldIndex);
              tabs.insert(newIndex, temp);
              setState(() {});
              return false;
            },
          ),
        ),
        floatingActionButton: FloatingActionButton(
          child: Icon(Icons.add),
          onPressed: () {
            tabs.add(index.toString());
            setState(() {
              ++index;
            });
          },
        ),
        body: TabBarView(
          children: tabs.map((e) {
            return Center(
              child: (e + ". Page").text,
            );
          }).toList(),
        ),
      ),
    );
  }
}


```

