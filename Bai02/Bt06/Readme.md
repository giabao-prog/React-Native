LINK BAI: https://snack.expo.dev/@trangiabao/hazardous-blue-sandwich

App.js

là thành phần chính của ứng dụng ScheduleApp. File này quản lý dữ liệu lịch học, ngày đang được chọn và danh sách môn học hiển thị trên màn hình. App.js sử dụng useState để lưu ngày được chọn. Khi người dùng chọn một ngày khác, ứng dụng sẽ lấy dữ liệu lịch học của ngày đó và cập nhật giao diện. App.js cũng kiểm tra ngày được chọn có lịch học hay không. Nếu có lịch học thì hiển thị danh sách các môn học bằng ScheduleCard, nếu không có lịch học thì hiển thị thông báo không có lịch học.
```
code
import React, { useState } from 'react';
import {
  View,
  Text,
  StyleSheet,
  ScrollView,
  SafeAreaView
} from 'react-native';

import Header from './components/Header';
import DaySelector from './components/DaySelector';
import ScheduleCard from './components/ScheduleCard';

export default function App() {
  const [selectedDay, setSelectedDay] = useState('T2');

  const scheduleData = {
    T2: [
      {
        subject: 'Lập trình React Native',
        room: 'Phòng A101',
        time: '07:30 - 09:30',
        teacher: 'GV.Trần Ngọc Minh',
        color: '#4F46E5'
      },
      {
        subject: 'Cơ sở dữ liệu',
        room: 'Phòng A203',
        time: '13:30 - 15:30',
        teacher: 'GV. Trần Bình',
        color: '#16A34A'
      }
    ],

    T3: [
      {
        subject: 'Lập trình C#',
        room: 'Phòng B102',
        time: '07:30 - 09:30',
        teacher: 'GV.Nguyễn Thanh Hải',
        color: '#EA580C'
      }
    ],

    T4: [
      {
        subject: 'Thiết kế đồ họa',
        room: 'Phòng C201',
        time: '09:30 - 11:30',
        teacher: 'GV.Hồ Thị Thanh Diệu',
        color: '#DB2777'
      },
      {
        subject: 'Mạng máy tính',
        room: 'Phòng B205',
        time: '13:30 - 15:30',
        teacher: 'GV. Nguyễn Thị Thương',
        color: '#0891B2'
      }
    ],

    T5: [
      {
        subject: 'Phát triển ứng dụng Web',
        room: 'Phòng A105',
        time: '07:30 - 09:30',
        teacher: 'GV. Trần Ngọc Minh',
        color: '#7C3AED'
      }
    ],

    T6: [
      {
        subject: 'Lập trình Python',
        room: 'Phòng B301',
        time: '09:30 - 11:30',
        teacher: 'GV. Nguyễn Thanh Hải',
        color: '#CA8A04'
      }
    ],

    T7: [
      {
        subject: 'An toàn thông tin',
        room: 'Phòng C102',
        time: '07:30 - 09:30',
        teacher: 'GV. Thành Công',
        color: '#DC2626'
      }
    ],

    CN: []
  };

  const schedules = scheduleData[selectedDay];

  return (
    <SafeAreaView style={styles.container}>
      <Header />

      <ScrollView showsVerticalScrollIndicator={false}>
        <View style={styles.content}>

          <Text style={styles.title}>
            Lịch học trong tuần
          </Text>

          <Text style={styles.subtitle}>
            Chọn ngày để xem lịch học
          </Text>

          <DaySelector
            selectedDay={selectedDay}
            onSelectDay={setSelectedDay}
          />

          <Text style={styles.dayTitle}>
            Lịch học {selectedDay}
          </Text>

          {schedules.length > 0 ? (
            schedules.map((item, index) => (
              <ScheduleCard
                key={index}
                subject={item.subject}
                room={item.room}
                time={item.time}
                teacher={item.teacher}
                color={item.color}
              />
            ))
          ) : (
            <View style={styles.emptyBox}>
              <Text style={styles.emptyIcon}>
                📚
              </Text>

              <Text style={styles.emptyTitle}>
                Không có lịch học
              </Text>

              <Text style={styles.emptyText}>
                Ngày {selectedDay} hiện chưa có môn học.
              </Text>
            </View>
          )}

        </View>
      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#F3F4F6'
  },

  content: {
    padding: 16,
    paddingBottom: 30
  },

  title: {
    fontSize: 24,
    fontWeight: 'bold',
    color: '#111827',
    marginTop: 10
  },

  subtitle: {
    fontSize: 14,
    color: '#6B7280',
    marginTop: 5,
    marginBottom: 18
  },

  dayTitle: {
    fontSize: 20,
    fontWeight: 'bold',
    color: '#111827',
    marginTop: 25,
    marginBottom: 15
  },

  emptyBox: {
    backgroundColor: '#FFFFFF',
    borderRadius: 16,
    padding: 30,
    alignItems: 'center',
    marginTop: 10
  },

  emptyIcon: {
    fontSize: 45,
    marginBottom: 10
  },

  emptyTitle: {
    fontSize: 19,
    fontWeight: 'bold',
    color: '#374151'
  },

  emptyText: {
    fontSize: 14,
    color: '#6B7280',
    marginTop: 7,
    textAlign: 'center'
  }
});
```

Header.js

là component dùng để tạo phần đầu của ứng dụng. Component này hiển thị tên ứng dụng ScheduleApp, tên sinh viên Trần Gia Bảo và biểu tượng lịch. Header giúp giao diện có phần tiêu đề rõ ràng và giúp người dùng nhận biết thông tin của ứng dụng.
```
code
import React from 'react';
import {
  View,
  Text,
  StyleSheet
} from 'react-native';

export default function Header() {
  return (
    <View style={styles.header}>

      <View>
        <Text style={styles.appName}>
          TKB-Online
        </Text>

        <Text style={styles.student}>
          Sinh viên: Trần Gia Bảo
        </Text>
      </View>

      <Text style={styles.icon}>
        📅
      </Text>

    </View>
  );
}

const styles = StyleSheet.create({
  header: {
    backgroundColor: '#4F46E5',
    paddingHorizontal: 20,
    paddingVertical: 18,
    flexDirection: 'row',
    justifyContent: 'space-between',
    alignItems: 'center'
  },

  appName: {
    color: '#FFFFFF',
    fontSize: 22,
    fontWeight: 'bold'
  },

  student: {
    color: '#E0E7FF',
    fontSize: 13,
    marginTop: 4
  },

  icon: {
    fontSize: 32
  }
});
```

DaySelector.js

là component dùng để hiển thị 7 ngày trong tuần gồm T2, T3, T4, T5, T6, T7 và CN. Người dùng có thể nhấn vào từng ngày để xem lịch học tương ứng. Ngày đang được chọn sẽ được hiển thị bằng màu nổi bật. Khi người dùng chọn một ngày, DaySelector sẽ gửi ngày được chọn về App.js để cập nhật danh sách lịch học.
```
code
import React from 'react';
import {
  View,
  Text,
  TouchableOpacity,
  StyleSheet
} from 'react-native';

export default function DaySelector({
  selectedDay,
  onSelectDay
}) {

  const days = [
    'T2',
    'T3',
    'T4',
    'T5',
    'T6',
    'T7',
    'CN'
  ];

  return (
    <View style={styles.container}>

      {days.map((day) => (
        <TouchableOpacity
          key={day}
          style={[
            styles.dayButton,
            selectedDay === day && styles.selectedDay
          ]}
          onPress={() => onSelectDay(day)}
        >

          <Text
            style={[
              styles.dayText,
              selectedDay === day && styles.selectedText
            ]}
          >
            {day}
          </Text>

        </TouchableOpacity>
      ))}

    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    backgroundColor: '#FFFFFF',
    padding: 8,
    borderRadius: 15
  },

  dayButton: {
    width: 42,
    height: 42,
    borderRadius: 12,
    justifyContent: 'center',
    alignItems: 'center'
  },

  selectedDay: {
    backgroundColor: '#4F46E5'
  },

  dayText: {
    fontSize: 14,
    fontWeight: '600',
    color: '#6B7280'
  },

  selectedText: {
    color: '#FFFFFF'
  }
});
```

ScheduleCard.js

là component dùng để hiển thị thông tin của một môn học. Mỗi thẻ lịch học hiển thị tên môn học, giờ học, phòng học và giảng viên. Component nhận dữ liệu từ App.js và hiển thị thông tin dưới dạng một thẻ riêng biệt. Mỗi môn học được sử dụng một màu khác nhau để giúp người dùng dễ dàng phân biệt các môn học.
```
code
import React from 'react';
import {
  View,
  Text,
  StyleSheet
} from 'react-native';

export default function ScheduleCard({
  subject,
  room,
  time,
  teacher,
  color
}) {
  return (
    <View style={styles.card}>

      <View
        style={[
          styles.colorBar,
          { backgroundColor: color }
        ]}
      />

      <View style={styles.content}>

        <Text style={styles.subject}>
          {subject}
        </Text>

        <View style={styles.info}>
          <Text style={styles.icon}>
            🕐
          </Text>

          <Text style={styles.text}>
            {time}
          </Text>
        </View>

        <View style={styles.info}>
          <Text style={styles.icon}>
            📍
          </Text>

          <Text style={styles.text}>
            {room}
          </Text>
        </View>

        <View style={styles.info}>
          <Text style={styles.icon}>
            👨‍🏫
          </Text>

          <Text style={styles.text}>
            {teacher}
          </Text>
        </View>

      </View>

    </View>
  );
}

const styles = StyleSheet.create({
  card: {
    backgroundColor: '#FFFFFF',
    borderRadius: 16,
    marginBottom: 15,
    flexDirection: 'row',
    overflow: 'hidden',
    elevation: 3
  },

  colorBar: {
    width: 7
  },

  content: {
    padding: 17,
    flex: 1
  },

  subject: {
    fontSize: 18,
    fontWeight: 'bold',
    color: '#111827',
    marginBottom: 12
  },

  info: {
    flexDirection: 'row',
    alignItems: 'center',
    marginTop: 7
  },

  icon: {
    width: 28,
    fontSize: 16
  },

  text: {
    fontSize: 14,
    color: '#4B5563'
  }
});
```

KET QUA CUOI CUNG

<img width="421" height="725" alt="image" src="https://github.com/user-attachments/assets/d52c98c5-041d-4a9c-8f2c-39dd98e266e4" />

<img width="419" height="684" alt="image" src="https://github.com/user-attachments/assets/e4f9fce2-89cd-48f1-91e0-d368c0ee96d8" />

<img width="420" height="720" alt="image" src="https://github.com/user-attachments/assets/3eade4ed-98a9-4061-9464-7e67f090f695" />

<img width="422" height="727" alt="image" src="https://github.com/user-attachments/assets/80ca346b-e24f-46cb-b8d0-a00a15f127a0" />

<img width="422" height="727" alt="image" src="https://github.com/user-attachments/assets/b468dc34-d196-4c33-b9ce-cda95731c714" />

<img width="425" height="725" alt="image" src="https://github.com/user-attachments/assets/15947a17-74e7-4599-8112-1e96f273c812" />

<img width="422" height="721" alt="image" src="https://github.com/user-attachments/assets/aca6a31c-4070-4296-ac79-96dd427d76bc" />






