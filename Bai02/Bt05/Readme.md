link bai: https://snack.expo.dev/@trangiabao/animateapp?

App.js 

là file chính của ứng dụng React Native, có nhiệm vụ kết nối và điều khiển các Component trong ứng dụng. File này quản lý trạng thái của tiến độ học tập thông qua useState, trong đó progress dùng để lưu phần trăm tiến độ và started dùng để xác định người dùng đã bắt đầu hay chưa. Khi người dùng nhấn nút Bắt đầu học, hàm handleStart() được thực hiện để cập nhật tiến độ lên 100% và hiển thị thông báo hoàn thành. App.js đồng thời gọi và truyền dữ liệu cho ba Component gồm ProgressCard, ActionButton và AnimatedMessage.
```
code
import React, { useState } from 'react';
import {
  View,
  Text,
  StyleSheet
} from 'react-native';

import ProgressCard from './components/ProgressCard';
import ActionButton from './components/ActionButton';
import AnimatedMessage from './components/AnimatedMessage';

export default function App() {
  const [progress, setProgress] = useState(40);
  const [started, setStarted] = useState(false);

  const handleStart = () => {
    setStarted(true);
    setProgress(100);
  };

  return (
    <View style={styles.container}>
      <Text style={styles.title}>
        AnimateApp
      </Text>

      <Text style={styles.subtitle}>
        Theo dõi mục tiêu học tập
      </Text>

      <ProgressCard progress={progress} />

      <ActionButton
        onPress={handleStart}
        started={started}
      />

      <AnimatedMessage visible={started} />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#F4F7FB',
    padding: 20,
    paddingTop: 70
  },

  title: {
    fontSize: 30,
    fontWeight: 'bold',
    textAlign: 'center',
    color: '#1E3A8A'
  },

  subtitle: {
    fontSize: 16,
    textAlign: 'center',
    color: '#666',
    marginTop: 8,
    marginBottom: 30
  }
});
```

ProgressCard.js

là Component dùng để hiển thị thông tin về mục tiêu học tập và tiến độ thực hiện. Component nhận dữ liệu progress từ App.js thông qua Props. Dữ liệu này được sử dụng để thay đổi chiều dài của thanh tiến độ và hiển thị phần trăm hoàn thành. ProgressCard giúp giao diện được chia thành từng phần riêng biệt, dễ quản lý và có thể tái sử dụng cho nhiều mục tiêu khác nhau.
```
code
import React from 'react';
import {
  View,
  Text,
  StyleSheet
} from 'react-native';

export default function ProgressCard({ progress }) {
  return (
    <View style={styles.card}>
      <Text style={styles.title}>
        Mục tiêu hôm nay
      </Text>

      <Text style={styles.goal}>
        Học React Native
      </Text>

      <View style={styles.progressBackground}>
        <View
          style={[
            styles.progress,
            { width: `${progress}%` }
          ]}
        />
      </View>

      <Text style={styles.percent}>
        {progress}% hoàn thành
      </Text>
    </View>
  );
}

const styles = StyleSheet.create({
  card: {
    backgroundColor: '#FFFFFF',
    padding: 22,
    borderRadius: 18,
    elevation: 5,
    marginBottom: 25
  },

  title: {
    fontSize: 16,
    color: '#777'
  },

  goal: {
    fontSize: 22,
    fontWeight: 'bold',
    marginTop: 8,
    marginBottom: 18,
    color: '#222'
  },

  progressBackground: {
    height: 15,
    backgroundColor: '#E5E7EB',
    borderRadius: 10,
    overflow: 'hidden'
  },

  progress: {
    height: 15,
    backgroundColor: '#2563EB',
    borderRadius: 10
  },

  percent: {
    marginTop: 12,
    textAlign: 'right',
    fontSize: 15,
    fontWeight: 'bold',
    color: '#2563EB'
  }
});
```

ActionButton.js 

là Component tạo nút điều khiển cho ứng dụng. Nút có chức năng bắt đầu thực hiện mục tiêu học tập. Khi người dùng nhấn nút, sự kiện onPress được gọi và truyền về App.js để cập nhật trạng thái. Component nhận thêm Props started để xác định trạng thái hiện tại. Khi chưa hoàn thành, nút hiển thị Bắt đầu học; khi hoàn thành, nút chuyển thành Đã hoàn thành.
```
code
import React from 'react';
import {
  TouchableOpacity,
  Text,
  StyleSheet
} from 'react-native';

export default function ActionButton({ onPress, started }) {
  return (
    <TouchableOpacity
      style={[
        styles.button,
        started && styles.completed
      ]}
      onPress={onPress}
      disabled={started}
    >
      <Text style={styles.text}>
        {started ? 'Đã hoàn thành' : 'Bắt đầu học'}
      </Text>
    </TouchableOpacity>
  );
}

const styles = StyleSheet.create({
  button: {
    backgroundColor: '#2563EB',
    padding: 16,
    borderRadius: 14,
    alignItems: 'center'
  },

  completed: {
    backgroundColor: '#16A34A'
  },

  text: {
    color: '#FFFFFF',
    fontSize: 17,
    fontWeight: 'bold'
  }
});
```

AnimatedMessage.js 

là Component chịu trách nhiệm hiển thị thông báo khi người dùng hoàn thành mục tiêu. Component sử dụng thư viện Animated của React Native để tạo hiệu ứng chuyển động. Khi visible chuyển thành true, thông báo sẽ xuất hiện với hiệu ứng phóng to và di chuyển từ dưới lên. Component sử dụng Animated.spring() để tạo hiệu ứng phóng to và Animated.timing() để tạo hiệu ứng di chuyển. Đây là Component thực hiện yêu cầu chính của bài về hiệu ứng animation.
```
code
  import React, { useEffect, useRef } from 'react';
import {
  Animated,
  Text,
  StyleSheet
} from 'react-native';

export default function AnimatedMessage({ visible }) {
  const scale = useRef(new Animated.Value(0)).current;
  const translateY = useRef(new Animated.Value(50)).current;

  useEffect(() => {
    if (visible) {
      Animated.parallel([
        Animated.spring(scale, {
          toValue: 1,
          friction: 5,
          tension: 80,
          useNativeDriver: true
        }),

        Animated.timing(translateY, {
          toValue: 0,
          duration: 500,
          useNativeDriver: true
        })
      ]).start();
    }
  }, [visible]);

  if (!visible) {
    return null;
  }

  return (
    <Animated.View
      style={[
        styles.message,
        {
          transform: [
            { scale: scale },
            { translateY: translateY }
          ]
        }
      ]}
    >
      <Text style={styles.icon}>
        🎉
      </Text>

      <Text style={styles.title}>
        Hoàn thành!
      </Text>

      <Text style={styles.text}>
        Bạn đã hoàn thành mục tiêu hôm nay.
      </Text>
    </Animated.View>
  );
}

const styles = StyleSheet.create({
  message: {
    marginTop: 30,
    backgroundColor: '#DCFCE7',
    padding: 22,
    borderRadius: 18,
    alignItems: 'center'
  },

  icon: {
    fontSize: 40,
    marginBottom: 8
  },

  title: {
    fontSize: 23,
    fontWeight: 'bold',
    color: '#15803D'
  },

  text: {
    marginTop: 6,
    fontSize: 15,
    color: '#166534',
    textAlign: 'center'
  }
});
```

ket qua

<img width="418" height="704" alt="image" src="https://github.com/user-attachments/assets/00bcc6b6-0a8b-4748-9b31-13acf2965554" />
<img width="419" height="722" alt="image" src="https://github.com/user-attachments/assets/783f45b8-38fc-4588-b312-8784636d5725" />

