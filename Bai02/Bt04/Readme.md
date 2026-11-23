link bai tap: https://snack.expo.dev/@trangiabao/multiscreenapp

App.js
là file chính của ứng dụng React Native, có nhiệm vụ khởi tạo và quản lý hệ thống điều hướng giữa các màn hình. Trong file sử dụng NavigationContainer để chứa toàn bộ hệ thống Navigation và createNativeStackNavigator để tạo Stack Navigation. App.js khai báo 3 màn hình gồm HomeScreen, ListScreen và DetailScreen. Người dùng có thể di chuyển từ màn hình trang chủ đến màn hình danh sách, sau đó chọn một sản phẩm để xem màn hình chi tiết. Đây là file kết nối các màn hình lại với nhau và giúp ứng dụng hoạt động theo đúng luồng điều hướng.
```
code
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';

import HomeScreen from './Screens/HomeScreen';
import ListScreen from './Screens/ListScreen';
import DetailScreen from './Screens/DetailScreen';
import ProfileScreen from './Screens/ProfileScreen';

const Stack = createNativeStackNavigator();
const Tab = createBottomTabNavigator();

function ListStack() {
  return (
    <Stack.Navigator>
      <Stack.Screen
        name="List"
        component={ListScreen}
        options={{ title: 'Danh sách' }}
      />

      <Stack.Screen
        name="Detail"
        component={DetailScreen}
        options={{ title: 'Chi tiết' }}
      />
    </Stack.Navigator>
  );
}

export default function App() {
  return (
    <NavigationContainer>
      <Tab.Navigator>
        <Tab.Screen
          name="Home"
          component={HomeScreen}
          options={{ title: 'Trang chủ' }}
        />

        <Tab.Screen
          name="ListTab"
          component={ListStack}
          options={{ title: 'Danh sách' }}
        />

        <Tab.Screen
          name="Profile"
          component={ProfileScreen}
          options={{ title: 'Cá nhân' }}
        />
      </Tab.Navigator>
    </NavigationContainer>
  );
}
```
HomeScreen.js
 là màn hình trang chủ của ứng dụng MultiScreenApp. Màn hình này hiển thị tên ứng dụng, nội dung giới thiệu và nút Xem danh sách. Khi người dùng nhấn nút, hàm navigation.navigate('List') được sử dụng để chuyển từ HomeScreen sang ListScreen. File này có nhiệm vụ tạo giao diện đầu tiên mà người dùng nhìn thấy khi mở ứng dụng và cung cấp chức năng bắt đầu sử dụng ứng dụng.

```
code
import React from 'react';
import {
  View,
  Text,
  TouchableOpacity,
  StyleSheet
} from 'react-native';

export default function HomeScreen({ navigation }) {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>
        MultiScreenApp
      </Text>

      <Text style={styles.text}>
        Ứng dụng quản lý sản phẩm
      </Text>

      <TouchableOpacity
        style={styles.button}
        onPress={() => navigation.navigate('ListTab')}
      >
        <Text style={styles.buttonText}>
          Xem danh sách
        </Text>
      </TouchableOpacity>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    padding: 20,
    backgroundColor: '#f3f4f6'
  },

  title: {
    fontSize: 30,
    fontWeight: 'bold',
    marginBottom: 15,
    color: '#2563eb'
  },

  text: {
    fontSize: 18,
    marginBottom: 30
  },

  button: {
    backgroundColor: '#2563eb',
    paddingVertical: 15,
    paddingHorizontal: 25,
    borderRadius: 10
  },

  buttonText: {
    color: 'white',
    fontSize: 16,
    fontWeight: 'bold'
  }
});
```

ListScreen.js
là màn hình hiển thị danh sách các sản phẩm trong ứng dụng. File sử dụng một mảng products để lưu thông tin của các sản phẩm như tên, danh mục, giá và mô tả. Hàm map() được sử dụng để duyệt qua danh sách sản phẩm và hiển thị từng sản phẩm thông qua component ItemCard. Khi người dùng chọn một sản phẩm, navigation.navigate('Detail', { product: item }) sẽ chuyển sang DetailScreen và truyền thông tin sản phẩm được chọn sang màn hình chi tiết. File này có nhiệm vụ quản lý và hiển thị danh sách sản phẩm.

```
code
import React from 'react';
import {
  View,
  Text,
  TouchableOpacity,
  StyleSheet,
  FlatList
} from 'react-native';

const products = [
  {
    id: '1',
    name: 'iPhone 17 Pro',
    price: '34.990.000đ',
    category: 'Điện thoại',
    description: 'Điện thoại cao cấp của Apple.'
  },
  {
    id: '2',
    name: 'Samsung Galaxy S25',
    price: '24.990.000đ',
    category: 'Điện thoại',
    description: 'Điện thoại Android cao cấp.'
  },
  {
    id: '3',
    name: 'MacBook Air M4',
    price: '29.990.000đ',
    category: 'Laptop',
    description: 'Laptop mỏng nhẹ dành cho học tập.'
  },
  {
    id: '4',
    name: 'ASUS Gaming',
    price: '25.990.000đ',
    category: 'Laptop',
    description: 'Laptop gaming mạnh mẽ.'
  }
];

export default function ListScreen({ navigation }) {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>
        Danh sách sản phẩm
      </Text>

      <FlatList
        data={products}
        keyExtractor={(item) => item.id}
        renderItem={({ item }) => (
          <TouchableOpacity
            style={styles.item}
            onPress={() =>
              navigation.navigate('Detail', {
                product: item
              })
            }
          >
            <Text style={styles.name}>
              {item.name}
            </Text>

            <Text style={styles.price}>
              {item.price}
            </Text>

            <Text style={styles.category}>
              {item.category}
            </Text>
          </TouchableOpacity>
        )}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 15,
    backgroundColor: '#f3f4f6'
  },

  title: {
    fontSize: 24,
    fontWeight: 'bold',
    marginBottom: 15
  },

  item: {
    backgroundColor: 'white',
    padding: 20,
    marginBottom: 12,
    borderRadius: 10,
    elevation: 3
  },

  name: {
    fontSize: 19,
    fontWeight: 'bold',
    marginBottom: 8
  },

  price: {
    fontSize: 17,
    color: '#2563eb',
    fontWeight: 'bold',
    marginBottom: 5
  },

  category: {
    color: '#666'
  }
});
```

DetailScreen.js
là màn hình hiển thị thông tin chi tiết của sản phẩm mà người dùng đã chọn ở ListScreen. File nhận dữ liệu sản phẩm thông qua route.params với câu lệnh const { product } = route.params. Sau đó các thông tin như tên sản phẩm, danh mục, giá và mô tả được hiển thị trên giao diện. Màn hình cũng có nút Quay lại, sử dụng navigation.goBack() để trở về màn hình trước đó. File này có nhiệm vụ cung cấp thông tin chi tiết và hỗ trợ người dùng quay lại danh sách.
```
code
import React from 'react';
import {
  View,
  Text,
  TouchableOpacity,
  StyleSheet
} from 'react-native';

export default function DetailScreen({ route, navigation }) {
  const { product } = route.params;

  return (
    <View style={styles.container}>
      <Text style={styles.title}>
        Chi tiết sản phẩm
      </Text>

      <Text style={styles.name}>
        {product.name}
      </Text>

      <Text style={styles.price}>
        {product.price}
      </Text>

      <Text style={styles.category}>
        Danh mục: {product.category}
      </Text>

      <Text style={styles.description}>
        {product.description}
      </Text>

      <TouchableOpacity
        style={styles.button}
        onPress={() => navigation.goBack()}
      >
        <Text style={styles.buttonText}>
          Quay lại
        </Text>
      </TouchableOpacity>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    padding: 20,
    backgroundColor: '#f3f4f6'
  },

  title: {
    fontSize: 24,
    fontWeight: 'bold',
    marginBottom: 25
  },

  name: {
    fontSize: 28,
    fontWeight: 'bold',
    marginBottom: 15
  },

  price: {
    fontSize: 22,
    color: '#2563eb',
    fontWeight: 'bold',
    marginBottom: 15
  },

  category: {
    fontSize: 17,
    marginBottom: 15
  },

  description: {
    fontSize: 16,
    textAlign: 'center',
    marginBottom: 30
  },

  button: {
    backgroundColor: '#2563eb',
    paddingVertical: 15,
    paddingHorizontal: 35,
    borderRadius: 10
  },

  buttonText: {
    color: 'white',
    fontSize: 16,
    fontWeight: 'bold'
  }
});
```

ProfileScreen.js
là màn hình cá nhân của ứng dụng MultiScreenApp, dùng để hiển thị thông tin của người sử dụng ứng dụng. File sử dụng các thành phần View, Text và StyleSheet của React Native để xây dựng giao diện. Phần avatar tạo một hình tròn làm ảnh đại diện và hiển thị chữ cái B bên trong. Phần name hiển thị tên người dùng là Trần Gia Bảo. Các thành phần info hiển thị thông tin sinh viên, lớp học và tên ứng dụng. StyleSheet.create() được sử dụng để thiết lập giao diện như kích thước, màu sắc, căn giữa, khoảng cách và kích thước chữ. ProfileScreen có công dụng tạo một màn hình cá nhân riêng, giúp người dùng xem các thông tin cơ bản của mình trong ứng dụng.
```
code
import React from 'react';
import {
  View,
  Text,
  StyleSheet
} from 'react-native';

export default function ProfileScreen() {
  return (
    <View style={styles.container}>
      <View style={styles.avatar}>
        <Text style={styles.avatarText}>
          B
        </Text>
      </View>

      <Text style={styles.name}>
        Trần Gia Bảo
      </Text>

      <Text style={styles.info}>
        Sinh viên Công nghệ thông tin
      </Text>

      <Text style={styles.info}>
        Lớp: CĐ-CNTT18A06
      </Text>

      <Text style={styles.info}>
        Ứng dụng: MultiScreenApp
      </Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    padding: 20,
    backgroundColor: '#f3f4f6'
  },

  avatar: {
    width: 100,
    height: 100,
    borderRadius: 50,
    backgroundColor: '#2563eb',
    justifyContent: 'center',
    alignItems: 'center',
    marginBottom: 20
  },

  avatarText: {
    color: 'white',
    fontSize: 40,
    fontWeight: 'bold'
  },

  name: {
    fontSize: 25,
    fontWeight: 'bold',
    marginBottom: 10
  },

  info: {
    fontSize: 16,
    color: '#555',
    marginBottom: 10
  }
});
```
ket qua
<img width="417" height="715" alt="image" src="https://github.com/user-attachments/assets/92b684c7-9ab0-4690-b8d8-16bde3d53892" />
<img width="413" height="641" alt="image" src="https://github.com/user-attachments/assets/29843076-c35a-4750-979a-e5a09d126832" />
<img width="418" height="721" alt="image" src="https://github.com/user-attachments/assets/8662e2eb-a5dc-42e5-aca1-cdfc08821d3a" />



