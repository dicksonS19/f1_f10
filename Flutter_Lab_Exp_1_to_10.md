# 24CS2016 Flutter Lab – Programs for Experiments 1 to 10


---

## Exp 1 – Basic Application Building using Flutter

### Commands

```bash
flutter doctor
flutter devices
flutter create widget_layout
cd widget_layout
code .
flutter run -d chrome
```

### lib/main.dart

```dart
import 'package:flutter/material.dart';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: Scaffold(
        appBar: AppBar(
          title: const Text('Student Profile'),
          backgroundColor: Colors.blue,
          foregroundColor: Colors.white,
        ),
        body: ListView(
          padding: const EdgeInsets.all(10),
          children: [
            Container(
              padding: const EdgeInsets.all(20),
              margin: const EdgeInsets.all(10),
              decoration: BoxDecoration(
                color: Colors.blue.shade50,
                borderRadius: BorderRadius.circular(10),
                border: Border.all(color: Colors.blue.shade100),
              ),
              child: const Column(
                children: [
                  Text('Student Profile',
                      style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold)),
                  SizedBox(height: 10),
                  Text('Raj', style: TextStyle(fontSize: 18)),
                  Text('CSE', style: TextStyle(fontSize: 16, color: Colors.grey)),
                  SizedBox(height: 5),
                  Text('Computer Science and Engineering'),
                  Text('Flutter Laboratory'),
                ],
              ),
            ),
            const SizedBox(height: 15),
            const Row(
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              children: [
                Icon(Icons.home, size: 30, color: Colors.blue),
                Icon(Icons.person, size: 30, color: Colors.blue),
                Icon(Icons.settings, size: 30, color: Colors.blue),
              ],
            ),
            const SizedBox(height: 20),
            const Card(
              elevation: 4,
              margin: EdgeInsets.symmetric(horizontal: 10, vertical: 5),
              child: ListTile(
                leading: Icon(Icons.book, color: Colors.orange),
                title: Text('Flutter'),
                subtitle: Text('Mobile Application Development'),
              ),
            ),
            const Card(
              elevation: 2,
              margin: EdgeInsets.symmetric(horizontal: 10, vertical: 5),
              child: ListTile(
                leading: Icon(Icons.cloud, color: Colors.indigo),
                title: Text('Cloud Computing'),
                subtitle: Text('Distributed Architecture'),
              ),
            ),
            const Card(
              elevation: 2,
              margin: EdgeInsets.symmetric(horizontal: 10, vertical: 5),
              child: ListTile(
                leading: Icon(Icons.code, color: Colors.green),
                title: Text('Programming'),
                subtitle: Text('Core Engineering Development'),
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```


---

## Exp 2 – Adaptive and Responsive UI Design

### Commands

```bash
flutter create responsive_ui
cd responsive_ui
code .
flutter run -d chrome
```

### lib/main.dart

```dart
import 'package:flutter/material.dart';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: Scaffold(
        appBar: AppBar(title: const Text('Responsive UI')),
        body: LayoutBuilder(
          builder: (context, constraints) {
            if (constraints.maxWidth < 600) {
              // Mobile layout: cards stacked vertically
              return const Column(
                children: [
                  Card(child: ListTile(title: Text('Student'))),
                  Card(child: ListTile(title: Text('Courses'))),
                ],
              );
            } else {
              // Tablet / desktop layout: cards side by side
              return const Row(
                children: [
                  Expanded(child: Card(child: ListTile(title: Text('Students')))),
                  Expanded(child: Card(child: ListTile(title: Text('Courses')))),
                ],
              );
            }
          },
        ),
      ),
    );
  }
}
```


---

## Exp 3 – Add Interactivity to App (Input and Forms)

### Commands

```bash
flutter create student_form
cd student_form
code .
flutter run -d chrome
```

### lib/main.dart

```dart
import 'package:flutter/material.dart';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Student Form',
      theme: ThemeData(colorSchemeSeed: Colors.deepPurple, useMaterial3: true),
      home: const StudentForm(),
    );
  }
}

class StudentForm extends StatefulWidget {
  const StudentForm({super.key});

  @override
  State<StudentForm> createState() => _StudentFormState();
}

class _StudentFormState extends State<StudentForm> {
  final _formKey = GlobalKey<FormState>();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Student Registration Form'),
        backgroundColor: Theme.of(context).colorScheme.primary,
        foregroundColor: Colors.white,
      ),
      body: Padding(
        padding: const EdgeInsets.all(16),
        child: Form(
          key: _formKey,
          child: Column(
            children: [
              TextFormField(
                decoration: const InputDecoration(labelText: 'Student Name'),
                validator: (value) {
                  if (value == null || value.isEmpty) return 'Enter student name';
                  return null;
                },
              ),
              const SizedBox(height: 16),
              TextFormField(
                decoration: const InputDecoration(labelText: 'Email'),
                keyboardType: TextInputType.emailAddress,
                validator: (value) {
                  if (value == null || value.isEmpty) return 'Enter email';
                  if (!RegExp(r'^[^@\s]+@[^@\s]+\.[^@\s]+$').hasMatch(value)) {
                    return 'Enter a valid email';
                  }
                  return null;
                },
              ),
              const SizedBox(height: 16),
              TextFormField(
                obscureText: true,
                decoration: const InputDecoration(labelText: 'Password'),
                validator: (value) {
                  if (value == null || value.isEmpty) return 'Enter password';
                  if (value.length < 6) return 'Password must be at least 6 characters';
                  return null;
                },
              ),
              const SizedBox(height: 24),
              ElevatedButton(
                onPressed: () {
                  if (_formKey.currentState!.validate()) {
                    ScaffoldMessenger.of(context).showSnackBar(
                      const SnackBar(content: Text('Form submitted successfully')),
                    );
                  }
                },
                child: const Text('Submit'),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```


---

## Exp 4 – Utilize the Assets and Media

### Commands

```bash
flutter create media_app
cd media_app
mkdir assets\images assets\audio assets\video     # Windows
# mkdir -p assets/images assets/audio assets/video  # Linux / macOS
# copy flutter.png, sound.mp3, sample.mp4 into the matching folders

flutter pub add audioplayers video_player
flutter pub get
flutter run -d chrome
```

### pubspec.yaml (flutter section)

```yaml
flutter:
  uses-material-design: true
  assets:
    - assets/images/
    - assets/audio/
    - assets/video/
```

### Part 1 – lib/main.dart (image gallery)

```dart
import 'package:flutter/material.dart';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({super.key});
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(colorSchemeSeed: Colors.deepPurple, useMaterial3: true),
      home: Scaffold(
        appBar: AppBar(
          title: const Text('Image Gallery'),
          backgroundColor: Colors.deepPurple,
          foregroundColor: Colors.white,
        ),
        body: GridView.count(
          crossAxisCount: 2,
          padding: const EdgeInsets.all(8),
          crossAxisSpacing: 8,
          mainAxisSpacing: 8,
          children: [
            Image.asset('assets/images/flutter.png'),
            Image.asset('assets/images/flutter.png'),
            Image.asset('assets/images/flutter.png'),
            Image.asset('assets/images/flutter.png'),
          ],
        ),
      ),
    );
  }
}
```

### Part 2 – lib/main.dart (image + audio + video)

```dart
import 'package:audioplayers/audioplayers.dart';
import 'package:flutter/material.dart';
import 'package:video_player/video_player.dart';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({super.key});
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Media App',
      theme: ThemeData(colorSchemeSeed: Colors.deepPurple, useMaterial3: true),
      home: const MediaScreen(),
    );
  }
}

class MediaScreen extends StatefulWidget {
  const MediaScreen({super.key});
  @override
  State<MediaScreen> createState() => _MediaScreenState();
}

class _MediaScreenState extends State<MediaScreen> {
  final AudioPlayer _audioPlayer = AudioPlayer();
  late VideoPlayerController _videoController;
  bool _audioPlaying = false;

  @override
  void initState() {
    super.initState();
    _videoController = VideoPlayerController.asset('assets/video/sample.mp4')
      ..initialize().then((_) => setState(() {}));
  }

  @override
  void dispose() {
    _audioPlayer.dispose();
    _videoController.dispose();
    super.dispose();
  }

  Future<void> _toggleAudio() async {
    if (_audioPlaying) {
      await _audioPlayer.pause();
    } else {
      await _audioPlayer.play(AssetSource('audio/sound.mp3')); // no "assets/" prefix
    }
    setState(() => _audioPlaying = !_audioPlaying);
  }

  void _toggleVideo() {
    setState(() {
      _videoController.value.isPlaying
          ? _videoController.pause()
          : _videoController.play();
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Assets and Media'),
        backgroundColor: Colors.deepPurple,
        foregroundColor: Colors.white,
      ),
      body: SingleChildScrollView(
        padding: const EdgeInsets.all(16),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            const Text('Image Gallery',
                style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold)),
            const SizedBox(height: 8),
            GridView.count(
              crossAxisCount: 2,
              shrinkWrap: true,
              physics: const NeverScrollableScrollPhysics(),
              crossAxisSpacing: 8,
              mainAxisSpacing: 8,
              children: [
                Image.asset('assets/images/flutter.png'),
                Image.asset('assets/images/flutter.png'),
              ],
            ),
            const SizedBox(height: 24),
            const Text('Audio',
                style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold)),
            const SizedBox(height: 8),
            ElevatedButton.icon(
              onPressed: _toggleAudio,
              icon: Icon(_audioPlaying ? Icons.pause : Icons.play_arrow),
              label: Text(_audioPlaying ? 'Pause Audio' : 'Play Audio'),
            ),
            const SizedBox(height: 24),
            const Text('Video',
                style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold)),
            const SizedBox(height: 8),
            _videoController.value.isInitialized
                ? AspectRatio(
                    aspectRatio: _videoController.value.aspectRatio,
                    child: VideoPlayer(_videoController),
                  )
                : const Center(child: CircularProgressIndicator()),
            const SizedBox(height: 8),
            ElevatedButton.icon(
              onPressed: _toggleVideo,
              icon: Icon(_videoController.value.isPlaying
                  ? Icons.pause
                  : Icons.play_arrow),
              label: Text(
                  _videoController.value.isPlaying ? 'Pause Video' : 'Play Video'),
            ),
          ],
        ),
      ),
    );
  }
}
```


---

## Exp 7 – Application State Management and Serialization

### Commands

```bash
flutter create state_app
cd state_app
code .
flutter run -d chrome
```

### lib/student.dart

```dart
class Student {
  final int id;
  final String name;
  final String course;

  Student({required this.id, required this.name, required this.course});

  // Serialization: object -> Map
  Map<String, dynamic> toJson() {
    return {
      'id': id,
      'name': name,
      'course': course,
    };
  }

  // Deserialization: Map -> object
  factory Student.fromJson(Map<String, dynamic> json) {
    return Student(
      id: json['id'],
      name: json['name'],
      course: json['course'],
    );
  }
}
```

### lib/main.dart

```dart
import 'package:flutter/material.dart';
import 'student.dart';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      title: 'State App',
      home: StudentListPage(),
    );
  }
}

class StudentListPage extends StatefulWidget {
  const StudentListPage({super.key});

  @override
  State<StudentListPage> createState() => _StudentListPageState();
}

class _StudentListPageState extends State<StudentListPage> {
  List<String> students = ['Priya', 'Aman'];
  final TextEditingController _nameController = TextEditingController();

  @override
  void initState() {
    super.initState();
    Student student = Student(id: 1, name: 'Felci', course: 'CSE');
    Map<String, dynamic> data = student.toJson();
    print(data);                       // {id: 1, name: Felci, course: CSE}
    Student newStudent = Student.fromJson(data);
    print(newStudent.name);            // Felci
  }

  void _addStudent() {
    final name = _nameController.text.trim();
    if (name.isEmpty) return;
    setState(() {
      students.add(name);
    });
    _nameController.clear();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Student List')),
      body: Column(
        children: [
          Padding(
            padding: const EdgeInsets.all(12.0),
            child: Row(
              children: [
                Expanded(
                  child: TextField(
                    controller: _nameController,
                    decoration: const InputDecoration(
                      labelText: 'Enter student name',
                      border: OutlineInputBorder(),
                    ),
                  ),
                ),
                const SizedBox(width: 8),
                ElevatedButton(
                  onPressed: _addStudent,
                  child: const Icon(Icons.add),
                ),
              ],
            ),
          ),
          Expanded(
            child: ListView.builder(
              itemCount: students.length,
              itemBuilder: (context, index) {
                return ListTile(
                  leading: const Icon(Icons.person),
                  title: Text(students[index]),
                );
              },
            ),
          ),
        ],
      ),
    );
  }

  @override
  void dispose() {
    _nameController.dispose();
    super.dispose();
  }
}
```


---

## Exp 8 – Data Persistence using SQLite and Firebase

### Commands

```bash
flutter create sqlite_app
cd sqlite_app
flutter pub add sqflite path firebase_core cloud_firestore

# Firebase setup (create a project and a Firestore database in the Firebase Console first)
dart pub global activate flutterfire_cli
flutterfire configure

# sqflite does not run in Chrome - use an Android emulator
flutter run
```

### lib/main.dart

```dart
import 'package:flutter/material.dart';
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';
import 'package:firebase_core/firebase_core.dart';
import 'package:cloud_firestore/cloud_firestore.dart';
import 'firebase_options.dart';

Future<void> main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp(options: DefaultFirebaseOptions.currentPlatform);
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});
  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      title: 'SQLite + Firebase App',
      home: HomePage(),
    );
  }
}

// ---------- SQLite helper (Part A) ----------
class DatabaseHelper {
  static final DatabaseHelper instance = DatabaseHelper._internal();
  DatabaseHelper._internal();
  static Database? _db;

  Future<Database> get database async {
    if (_db != null) return _db!;
    _db = await _initDatabase();
    return _db!;
  }

  Future<Database> _initDatabase() async {
    final path = join(await getDatabasesPath(), 'students.db');
    return await openDatabase(
      path,
      version: 1,
      onCreate: (db, version) async {
        await db.execute('''
          CREATE TABLE students (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            name TEXT NOT NULL,
            course TEXT NOT NULL
          )
        ''');
      },
    );
  }

  Future<int> insertStudent(Map<String, dynamic> s) async =>
      (await database).insert('students', s);

  Future<List<Map<String, dynamic>>> getStudents() async =>
      (await database).query('students', orderBy: 'id DESC');

  Future<int> updateStudent(int id, Map<String, dynamic> s) async =>
      (await database).update('students', s, where: 'id = ?', whereArgs: [id]);

  Future<int> deleteStudent(int id) async =>
      (await database).delete('students', where: 'id = ?', whereArgs: [id]);
}

// ---------- Home with tabs ----------
class HomePage extends StatelessWidget {
  const HomePage({super.key});
  @override
  Widget build(BuildContext context) {
    return DefaultTabController(
      length: 2,
      child: Scaffold(
        appBar: AppBar(
          title: const Text('Data Persistence Demo'),
          bottom: const TabBar(tabs: [
            Tab(text: 'SQLite (Local)'),
            Tab(text: 'Firebase (Cloud)'),
          ]),
        ),
        body: const TabBarView(children: [SqliteTab(), FirebaseTab()]),
      ),
    );
  }
}

// ---------- Part A: SQLite tab ----------
class SqliteTab extends StatefulWidget {
  const SqliteTab({super.key});
  @override
  State<SqliteTab> createState() => _SqliteTabState();
}

class _SqliteTabState extends State<SqliteTab> {
  final _nameController = TextEditingController();
  final _courseController = TextEditingController();
  List<Map<String, dynamic>> _students = [];
  int? _editingId;

  @override
  void initState() {
    super.initState();
    _refreshStudents();
  }

  Future<void> _refreshStudents() async {
    final data = await DatabaseHelper.instance.getStudents();
    setState(() => _students = data);
  }

  Future<void> _saveStudent() async {
    final name = _nameController.text.trim();
    final course = _courseController.text.trim();
    if (name.isEmpty || course.isEmpty) return;
    if (_editingId == null) {
      await DatabaseHelper.instance
          .insertStudent({'name': name, 'course': course});
    } else {
      await DatabaseHelper.instance
          .updateStudent(_editingId!, {'name': name, 'course': course});
      _editingId = null;
    }
    _nameController.clear();
    _courseController.clear();
    _refreshStudents();
  }

  void _editStudent(Map<String, dynamic> s) {
    setState(() {
      _editingId = s['id'];
      _nameController.text = s['name'];
      _courseController.text = s['course'];
    });
  }

  Future<void> _deleteStudent(int id) async {
    await DatabaseHelper.instance.deleteStudent(id);
    _refreshStudents();
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Padding(
          padding: const EdgeInsets.all(12.0),
          child: Column(
            children: [
              TextField(
                controller: _nameController,
                decoration: const InputDecoration(labelText: 'Name'),
              ),
              TextField(
                controller: _courseController,
                decoration: const InputDecoration(labelText: 'Course'),
              ),
              const SizedBox(height: 8),
              ElevatedButton(
                onPressed: _saveStudent,
                child: Text(_editingId == null ? 'Add student' : 'Update student'),
              ),
            ],
          ),
        ),
        Expanded(
          child: ListView.builder(
            itemCount: _students.length,
            itemBuilder: (context, index) {
              final s = _students[index];
              return ListTile(
                title: Text(s['name']),
                subtitle: Text(s['course']),
                trailing: Row(
                  mainAxisSize: MainAxisSize.min,
                  children: [
                    IconButton(
                        icon: const Icon(Icons.edit),
                        onPressed: () => _editStudent(s)),
                    IconButton(
                        icon: const Icon(Icons.delete),
                        onPressed: () => _deleteStudent(s['id'])),
                  ],
                ),
              );
            },
          ),
        ),
      ],
    );
  }

  @override
  void dispose() {
    _nameController.dispose();
    _courseController.dispose();
    super.dispose();
  }
}

// ---------- Part B: Firebase tab ----------
class FirebaseTab extends StatefulWidget {
  const FirebaseTab({super.key});
  @override
  State<FirebaseTab> createState() => _FirebaseTabState();
}

class _FirebaseTabState extends State<FirebaseTab> {
  final _nameController = TextEditingController();
  final _courseController = TextEditingController();
  final CollectionReference students =
      FirebaseFirestore.instance.collection('students');

  Future<void> _addStudent() async {
    final name = _nameController.text.trim();
    final course = _courseController.text.trim();
    if (name.isEmpty || course.isEmpty) return;
    await students.add({'name': name, 'course': course});
    _nameController.clear();
    _courseController.clear();
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Padding(
          padding: const EdgeInsets.all(12.0),
          child: Column(
            children: [
              TextField(
                controller: _nameController,
                decoration: const InputDecoration(labelText: 'Name'),
              ),
              TextField(
                controller: _courseController,
                decoration: const InputDecoration(labelText: 'Course'),
              ),
              const SizedBox(height: 8),
              ElevatedButton(
                  onPressed: _addStudent, child: const Text('Add student')),
            ],
          ),
        ),
        Expanded(
          child: StreamBuilder<QuerySnapshot>(
            stream: students.snapshots(),
            builder: (context, snapshot) {
              if (!snapshot.hasData) {
                return const Center(child: CircularProgressIndicator());
              }
              final docs = snapshot.data!.docs;
              return ListView.builder(
                itemCount: docs.length,
                itemBuilder: (context, index) {
                  final data = docs[index].data() as Map<String, dynamic>;
                  return ListTile(
                    title: Text(data['name'] ?? ''),
                    subtitle: Text(data['course'] ?? ''),
                  );
                },
              );
            },
          ),
        ),
      ],
    );
  }

  @override
  void dispose() {
    _nameController.dispose();
    _courseController.dispose();
    super.dispose();
  }
}
```


---

## Exp 9 – Accessing APIs through HTTP

### Commands

```bash
flutter create api_app
cd api_app
flutter pub add http
flutter run -d chrome
```

### lib/main.dart

```dart
import 'dart:convert';
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({super.key});
  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      debugShowCheckedModeBanner: false,
      home: PostsPage(),
    );
  }
}

class PostsPage extends StatefulWidget {
  const PostsPage({super.key});
  @override
  State<PostsPage> createState() => _PostsPageState();
}

class _PostsPageState extends State<PostsPage> {
  late Future<List<dynamic>> futurePosts;

  Future<List<dynamic>> fetchData() async {
    final response = await http.get(
      Uri.parse('https://jsonplaceholder.typicode.com/posts'),
    );
    if (response.statusCode == 200) {
      return jsonDecode(response.body);
    } else {
      throw Exception('Failed to load data');
    }
  }

  @override
  void initState() {
    super.initState();
    futurePosts = fetchData();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('API data')),
      body: FutureBuilder<List<dynamic>>(
        future: futurePosts,
        builder: (context, snapshot) {
          if (snapshot.connectionState == ConnectionState.waiting) {
            return const Center(child: Text('Loading...'));
          } else if (snapshot.hasError) {
            return const Center(child: Text('Failed to load data'));
          }
          final data = snapshot.data!;
          return ListView.builder(
            itemCount: data.length,
            itemBuilder: (context, index) {
              return ListTile(title: Text(data[index]['title']));
            },
          );
        },
      ),
    );
  }
}
```


---

## Exp 10 – Add Android as a Build Target

### Commands

```bash
flutter doctor
flutter devices
flutter doctor --android-licenses

flutter create android_app
cd android_app
flutter run

flutter build apk
adb install build/app/outputs/flutter-apk/app-release.apk
```

APK location: `android_app/build/app/outputs/flutter-apk/app-release.apk`

### lib/main.dart

```dart
import 'package:flutter/material.dart';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({super.key});
  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      debugShowCheckedModeBanner: false,
      home: HomePage(),
    );
  }
}

class HomePage extends StatefulWidget {
  const HomePage({super.key});
  @override
  State<HomePage> createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  int _counter = 0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Flutter Android App')),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            const Text('You have pushed the button this many times:'),
            Text('$_counter', style: const TextStyle(fontSize: 32)),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () => setState(() => _counter++),
        child: const Icon(Icons.add),
      ),
    );
  }
}
```
