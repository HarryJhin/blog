---
title: Modal Navigation Drawer
description:
comments: true
---

# ModalNavigationDrawer

![material design navigation drawer](https://developer.android.com/images/reference/androidx/compose/material3/navigation-drawer.png)

```kotlin
@OptIn(ExperimentalMaterial3Api::class)
@Preview
@Sampled
@Composable
fun ModalNavigationDrawerSample() {
  val drawerState = rememberDrawerState(DrawerValue.Closed)
  val scope = rememberCoroutineScope()
  // icons to mimic drawer destinations
  val items = listOf(Icons.Default.Favorite, Icons.Default.Face, Icons.Default.Email)
  val selectedItem = remember { mutableStateOf(items[0]) }
  ModalNavigationDrawer(
  drawerState = drawerState,
  drawerContent = {
    ModalDrawerSheet {
      Spacer(Modifier.height(12.dp))
      items.forEach { item ->
        NavigationDrawerItem(
        icon = { Icon(item, contentDescription = null) },
        label = { Text(item.name) },
        selected = item == selectedItem.value,
        onClick = {
          scope.launch { drawerState.close() }
          selectedItem.value = item
          },
          modifier = Modifier.padding(NavigationDrawerItemDefaults.ItemPadding)
          )
          }
          }
          },
          content = {
            Column(
            modifier = Modifier
            .fillMaxSize()
            .padding(16.dp),
            horizontalAlignment = Alignment.CenterHorizontally
            ) {
              Text(text = if (drawerState.isClosed) ">>> Swipe >>>" else "<<< Swipe <<<")
              Spacer(Modifier.height(20.dp))
              Button(onClick = { scope.launch { drawerState.open() } }) {
                Text("Click to open")
                }
                }
                }
                )
                }

@OptIn(ExperimentalMaterial3Api::class)
@Preview
@Sampled
@Composable
fun PermanentNavigationDrawerSample() {
  // icons to mimic drawer destinations
  val items = listOf(Icons.Default.Favorite, Icons.Default.Face, Icons.Default.Email)
  val selectedItem = remember { mutableStateOf(items[0]) }
  PermanentNavigationDrawer(
  drawerContent = {
    PermanentDrawerSheet(Modifier.width(240.dp)) {
      Spacer(Modifier.height(12.dp))
      items.forEach { item ->
        NavigationDrawerItem(
        icon = { Icon(item, contentDescription = null) },
        label = { Text(item.name) },
        selected = item == selectedItem.value,
        onClick = {
          selectedItem.value = item
          },
          modifier = Modifier.padding(horizontal = 12.dp)
          )
          }
          }
          },
          content = {
            Column(
            modifier = Modifier
            .fillMaxSize()
            .padding(16.dp),
            horizontalAlignment = Alignment.CenterHorizontally
            ) {
              Text(text = "Application content")
              }
              }
              )
              }

@OptIn(ExperimentalMaterial3Api::class)
@Preview
@Sampled
@Composable
fun DismissibleNavigationDrawerSample() {
  val drawerState = rememberDrawerState(DrawerValue.Closed)
  val scope = rememberCoroutineScope()
  // icons to mimic drawer destinations
  val items = listOf(Icons.Default.Favorite, Icons.Default.Face, Icons.Default.Email)
  val selectedItem = remember { mutableStateOf(items[0]) }
  BackHandler(enabled = drawerState.isOpen) {
    scope.launch {
      drawerState.close()
      }
      }

DismissibleNavigationDrawer(
drawerState = drawerState,
drawerContent = {
  DismissibleDrawerSheet {
    Spacer(Modifier.height(12.dp))
    items.forEach { item ->
      NavigationDrawerItem(
      icon = { Icon(item, contentDescription = null) },
      label = { Text(item.name) },
      selected = item == selectedItem.value,
      onClick = {
        scope.launch { drawerState.close() }
        selectedItem.value = item
        },
        modifier = Modifier.padding(horizontal = 12.dp)
        )
        }
        }
        },
        content = {
          Column(
          modifier = Modifier
          .fillMaxSize()
          .padding(16.dp),
          horizontalAlignment = Alignment.CenterHorizontally
          ) {
            Text(text = if (drawerState.isClosed) ">>> Swipe >>>" else "<<< Swipe <<<")
            Spacer(Modifier.height(20.dp))
            Button(onClick = { scope.launch { drawerState.open() } }) {
              Text("Click to open")
              }
              }
              }
              )
              }

```
