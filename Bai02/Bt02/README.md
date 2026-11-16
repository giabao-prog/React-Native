Link bài
https://snack.expo.dev/@trangiabao/learningapp

App.js

Nội dung và vai trò
- Đây là tệp chính của ứng dụng LearningApp, có nhiệm vụ kết hợp và hiển thị các component đã được xây dựng gồm Header, StatCard, CourseCard và BottomMenu.
- Tệp này tổ chức bố cục tổng thể của trang Home, hiển thị phần thông tin sinh viên, thống kê học tập, danh sách các môn học và thanh menu ở cuối màn hình.
- App.js cũng truyền các dữ liệu như tên môn học, biểu tượng và phần trăm tiến độ vào các component tương ứng.

```
import { View, Text, StyleSheet, ScrollView } from 'react-native';

import Header from './components/Header';
import StatCard from './components/StatCard';
import CourseCard from './components/CourseCard';
import BottomMenu from './components/BottomMenu';

export default function App() {
  return (
    <View style={styles.container}>

      <ScrollView
        showsVerticalScrollIndicator={false}
        contentContainerStyle={styles.content}
      >

        <Header />

        <Text style={styles.sectionTitle}>
          Thống kê học tập
        </Text>

        <View style={styles.stats}>
          <StatCard
            number="12"
            title="Khóa học"
          />

          <StatCard
            number="5"
            title="Đang học"
          />

          <StatCard
            number="86%"
            title="Tiến độ"
          />
        </View>

        <Text style={styles.sectionTitle}>
          Môn học của tôi
        </Text>

        <CourseCard
          icon="📱"
          title="Lập trình Mobile"
          teacher="React Native"
          progress={85}
        />

        <CourseCard
          icon="💻"
          title="Lập trình Web"
          teacher="ASP.NET Core"
          progress={70}
        />

        <CourseCard
          icon="🗄️"
          title="Cơ sở dữ liệu"
          teacher="SQL Server"
          progress={90}
        />

        <CourseCard
          icon="🐍"
          title="Lập trình Python"
          teacher="Python cơ bản"
          progress={65}
        />

      </ScrollView>

      <BottomMenu />

    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#F5F5F5',
  },

  content: {
    paddingBottom: 20,
  },

  sectionTitle: {
    fontSize: 20,
    fontWeight: 'bold',
    marginTop: 20,
    marginBottom: 12,
    marginHorizontal: 15,
    color: '#222222',
  },

  stats: {
    flexDirection: 'row',
    paddingHorizontal: 10,
  },
});
```
Header.js

Nội dung và vai trò:
-Tệp Header.js có nhiệm vụ xây dựng phần đầu của trang Home. 
-Component này hiển thị lời chào người dùng, tên sinh viên, mã lớp và avatar.
-Header giúp người dùng nhận biết thông tin cá nhân ngay khi mở ứng dụng và tạo phần giao diện đầu tiên của trang Home.
```
import { View, Text, StyleSheet } from 'react-native';

export default function Header() {
  return (
    <View style={styles.container}>

      <View>
        <Text style={styles.welcome}>
          Xin chào 👋
        </Text>

        <Text style={styles.name}>
          Gia Bảo
        </Text>

        <Text style={styles.student}>
          CĐ-CNTT18A06
        </Text>
      </View>

      <View style={styles.avatar}>
        <Text style={styles.avatarText}>
          GB
        </Text>
      </View>

    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    alignItems: 'center',
    padding: 20,
    backgroundColor: '#FFD600',
    borderBottomLeftRadius: 25,
    borderBottomRightRadius: 25,
  },

  welcome: {
    fontSize: 16,
    color: '#333333',
  },

  name: {
    fontSize: 26,
    fontWeight: 'bold',
    color: '#000000',
  },

  student: {
    marginTop: 4,
    fontSize: 14,
    color: '#555555',
  },

  avatar: {
    width: 55,
    height: 55,
    borderRadius: 30,
    backgroundColor: '#000000',
    justifyContent: 'center',
    alignItems: 'center',
  },

  avatarText: {
    color: '#FFFFFF',
    fontSize: 18,
    fontWeight: 'bold',
  },
});
```
StatCard.js

Nội dung và vai trò:
- Tệp StatCard.js có nhiệm vụ tạo các thẻ thống kê thông tin học tập.
- Component hiển thị số liệu và tiêu đề tương ứng, chẳng hạn như số lượng khóa học, số khóa học đang học và phần trăm tiến độ.
- Component được thiết kế để có thể sử dụng nhiều lần với các dữ liệu khác nhau, giúp giảm việc lặp lại code.
```
import { View, Text, StyleSheet } from 'react-native';

export default function StatCard({ number, title }) {
  return (
    <View style={styles.card}>
      <Text style={styles.number}>{number}</Text>
      <Text style={styles.title}>{title}</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  card: {
    flex: 1,
    backgroundColor: '#FFFFFF',
    padding: 15,
    marginHorizontal: 5,
    borderRadius: 15,
    alignItems: 'center',
    elevation: 3,
    shadowColor: '#000',
    shadowOffset: {
      width: 0,
      height: 2,
    },
    shadowOpacity: 0.1,
    shadowRadius: 4,
  },

  number: {
    fontSize: 24,
    fontWeight: 'bold',
    color: '#000000',
  },

  title: {
    marginTop: 5,
    fontSize: 13,
    color: '#666666',
  },
});
```
CourseCard.js

Nội dung và vai trò:
- Tệp CourseCard.js có nhiệm vụ hiển thị thông tin của từng môn học trong ứng dụng.
- Mỗi CourseCard gồm biểu tượng môn học, tên môn học, nội dung hoặc công nghệ học tập và thanh tiến độ hoàn thành.
- Component nhận dữ liệu từ App.js và hiển thị các môn học như Lập trình Mobile, Lập trình Web, Cơ sở dữ liệu và Lập trình Python.
```
import { View, Text, StyleSheet } from 'react-native';

export default function CourseCard({
  icon,
  title,
  teacher,
  progress
}) {
  return (
    <View style={styles.card}>

      <View style={styles.iconBox}>
        <Text style={styles.icon}>
          {icon}
        </Text>
      </View>

      <View style={styles.info}>

        <Text style={styles.title}>
          {title}
        </Text>

        <Text style={styles.teacher}>
          {teacher}
        </Text>

        <View style={styles.progressBackground}>
          <View
            style={[
              styles.progress,
              {
                width: `${progress}%`,
              },
            ]}
          />
        </View>

        <Text style={styles.progressText}>
          {progress}% hoàn thành
        </Text>

      </View>

    </View>
  );
}

const styles = StyleSheet.create({
  card: {
    flexDirection: 'row',
    backgroundColor: '#FFFFFF',
    padding: 15,
    marginHorizontal: 15,
    marginBottom: 12,
    borderRadius: 15,
    elevation: 3,
    shadowColor: '#000000',
    shadowOffset: {
      width: 0,
      height: 2,
    },
    shadowOpacity: 0.1,
    shadowRadius: 4,
  },

  iconBox: {
    width: 55,
    height: 55,
    borderRadius: 12,
    backgroundColor: '#FFF3B0',
    justifyContent: 'center',
    alignItems: 'center',
  },

  icon: {
    fontSize: 27,
  },

  info: {
    flex: 1,
    marginLeft: 15,
  },

  title: {
    fontSize: 17,
    fontWeight: 'bold',
    color: '#222222',
  },

  teacher: {
    marginTop: 4,
    fontSize: 14,
    color: '#777777',
  },

  progressBackground: {
    height: 7,
    backgroundColor: '#EEEEEE',
    borderRadius: 5,
    marginTop: 10,
    overflow: 'hidden',
  },

  progress: {
    height: 7,
    backgroundColor: '#FFD600',
    borderRadius: 5,
  },

  progressText: {
    marginTop: 5,
    fontSize: 12,
    color: '#777777',
  },
});
```
BottomMenu.js

Nội dung và vai trò:
- Tệp BottomMenu.js có nhiệm vụ tạo thanh menu giả lập ở cuối màn hình ứng dụng.
- Thanh menu gồm ba mục Home, Courses và Profile cùng với các biểu tượng tương ứng.
- Component này giúp hoàn thiện bố cục trang Home và mô phỏng thanh điều hướng của một ứng dụng học tập.
```
import { View, Text, StyleSheet } from 'react-native';

export default function BottomMenu() {
  return (
    <View style={styles.container}>

      <View style={styles.item}>
        <Text style={styles.icon}>
          🏠
        </Text>

        <Text style={styles.active}>
          Home
        </Text>
      </View>

      <View style={styles.item}>
        <Text style={styles.icon}>
          📚
        </Text>

        <Text style={styles.text}>
          Courses
        </Text>
      </View>

      <View style={styles.item}>
        <Text style={styles.icon}>
          👤
        </Text>

        <Text style={styles.text}>
          Profile
        </Text>
      </View>

    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flexDirection: 'row',
    justifyContent: 'space-around',
    alignItems: 'center',
    backgroundColor: '#FFFFFF',
    paddingVertical: 12,
    borderTopWidth: 1,
    borderTopColor: '#EEEEEE',
  },

  item: {
    alignItems: 'center',
  },

  icon: {
    fontSize: 22,
  },

  active: {
    marginTop: 3,
    color: '#000000',
    fontWeight: 'bold',
  },

  text: {
    marginTop: 3,
    color: '#777777',
  },
});
```
Kết quả hiển thị

<img width="327" height="610" alt="image" src="https://github.com/user-attachments/assets/eb575314-0834-439b-919b-a139d5f7410a" />
