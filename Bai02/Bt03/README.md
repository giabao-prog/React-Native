Link bài làm:
https://snack.expo.dev/@trangiabao/productapp

File App.js

File App.js là file chính của ứng dụng ProductApp, có vai trò xây dựng giao diện chính, quản lý danh sách sản phẩm và hiển thị danh sách sản phẩm lên màn hình. Trong file này, thư viện React Native được sử dụng để tạo giao diện, FlatList được sử dụng để hiển thị danh sách sản phẩm và component ProductCard được import để hiển thị từng sản phẩm.

Phần import ở đầu file có nhiệm vụ đưa các thành phần cần thiết vào ứng dụng như SafeAreaView, View, Text, FlatList, StyleSheet, StatusBar và component ProductCard. Nhờ đó, ứng dụng có thể sử dụng các thành phần giao diện và chức năng cần thiết.

Phần const products dùng để lưu trữ dữ liệu của các sản phẩm. Mỗi sản phẩm gồm các thông tin như id, name, image, price và description. Đây là nguồn dữ liệu được sử dụng để hiển thị 6 sản phẩm trong ứng dụng.

Phần export default function App() là component chính của ứng dụng. Bên trong component này sử dụng SafeAreaView để tạo vùng hiển thị an toàn trên thiết bị. StatusBar được sử dụng để thiết lập màu sắc cho thanh trạng thái. Phần header tạo tiêu đề của ứng dụng với tên ProductApp và dòng giới thiệu "Cửa hàng sách online".

Phần FlatList có nhiệm vụ lấy dữ liệu từ mảng products và hiển thị danh sách sản phẩm. Thuộc tính data nhận danh sách sản phẩm, keyExtractor sử dụng id để xác định từng sản phẩm và renderItem dùng để hiển thị từng sản phẩm thông qua component ProductCard.

Trong renderItem, các dữ liệu của sản phẩm được truyền từ App.js sang ProductCard thông qua props gồm name, image, price và description. Cách làm này giúp có thể sử dụng lại cùng một component để hiển thị nhiều sản phẩm khác nhau.

Phần StyleSheet.create() dùng để thiết lập giao diện cho ứng dụng như màu nền, kích thước chữ, khoảng cách, màu sắc, phần tiêu đề và danh sách sản phẩm. Nhờ phần StyleSheet, giao diện ProductApp được thiết kế rõ ràng, dễ nhìn và phù hợp với ứng dụng bán sách.

```````
code
import React from 'react';
import {
  SafeAreaView,
  View,
  Text,
  FlatList,
  StyleSheet,
  StatusBar,
} from 'react-native';

import ProductCard from './components/ProductCard';

const products = [
  {
    id: '1',
    name: 'Đắc Nhân Tâm',
    image:
      'https://images.unsplash.com/photo-1544947950-fa07a98d237f?w=500',
    price: 86000,
    description:
      'Cuốn sách nổi tiếng về nghệ thuật giao tiếp và ứng xử trong cuộc sống.',
  },

  {
    id: '2',
    name: 'Nhà Giả Kim',
    image:
      'https://images.unsplash.com/photo-1512820790803-83ca734da794?w=500',
    price: 79000,
    description:
      'Câu chuyện truyền cảm hứng về hành trình theo đuổi ước mơ.',
  },

  {
    id: '3',
    name: 'Tuổi Trẻ Đáng Giá Bao Nhiêu',
    image:
      'https://images.unsplash.com/photo-1543002588-bfa74002ed7e?w=500',
    price: 95000,
    description:
      'Cuốn sách dành cho những người trẻ muốn phát triển bản thân.',
  },

  {
    id: '4',
    name: 'Atomic Habits',
    image:
      'https://images.unsplash.com/photo-1495446815901-a7297e633e8d?w=500',
    price: 120000,
    description:
      'Hướng dẫn xây dựng những thói quen tốt và thay đổi cuộc sống.',
  },

  {
    id: '5',
    name: 'Không Diệt Không Sinh Đừng Sợ Hãi',
    image:
      'https://images.unsplash.com/photo-1519682337058-a94d519337bc?w=500',
    price: 90000,
    description:
      'Cuốn sách giúp người đọc có góc nhìn tích cực hơn về cuộc sống.',
  },

  {
    id: '6',
    name: 'Hoàng Tử Bé',
    image:
      'https://images.unsplash.com/photo-1521587760476-6c12a4b040da?w=500',
    price: 65000,
    description:
      'Tác phẩm kinh điển với nhiều bài học ý nghĩa về tình yêu và cuộc sống.',
  },
];

export default function App() {
  return (
    <SafeAreaView style={styles.container}>
      <StatusBar
        barStyle="light-content"
        backgroundColor="#222222"
      />

      <View style={styles.header}>
        <Text style={styles.title}>
          📚 Bảo Mọt Sách
        </Text>

        <Text style={styles.subtitle}>
          Cửa hàng sách online
        </Text>
      </View>

      <View style={styles.content}>
        <Text style={styles.heading}>
          Sản phẩm nổi bật
        </Text>

        <FlatList
          data={products}
          keyExtractor={(item) => item.id}
          renderItem={({ item }) => (
            <ProductCard
              name={item.name}
              image={item.image}
              price={item.price}
              description={item.description}
            />
          )}
          showsVerticalScrollIndicator={false}
          contentContainerStyle={styles.list}
        />
      </View>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#f3f4f6',
  },

  header: {
    backgroundColor: '#222222',
    paddingHorizontal: 20,
    paddingTop: 20,
    paddingBottom: 20,
  },

  title: {
    color: '#ffffff',
    fontSize: 28,
    fontWeight: 'bold',
  },

  subtitle: {
    color: '#dddddd',
    fontSize: 15,
    marginTop: 5,
  },

  content: {
    flex: 1,
    paddingHorizontal: 15,
    paddingTop: 15,
  },

  heading: {
    fontSize: 22,
    fontWeight: 'bold',
    color: '#222222',
    marginBottom: 12,
  },

  list: {
    paddingBottom: 20,
  },
});

````````
File ProductCard.js

File ProductCard.js là một component riêng dùng để tạo giao diện cho một sản phẩm. Component này được thiết kế theo dạng có thể tái sử dụng nhiều lần. Thay vì phải viết lại giao diện cho từng sản phẩm, ProductCard nhận dữ liệu từ App.js thông qua props và hiển thị sản phẩm tương ứng.

Phần import ở đầu file sử dụng React và các thành phần của React Native gồm View, Text, Image và StyleSheet. View dùng để tạo vùng chứa, Text dùng để hiển thị nội dung chữ, Image dùng để hiển thị hình ảnh sản phẩm và StyleSheet dùng để thiết kế giao diện.

Phần const ProductCard = ({ name, image, price, description }) định nghĩa component ProductCard và nhận dữ liệu thông qua props. Các props gồm name là tên sản phẩm, image là đường dẫn hình ảnh, price là giá sản phẩm và description là mô tả sản phẩm.

Phần Image có nhiệm vụ hiển thị hình ảnh của sản phẩm dựa trên dữ liệu được truyền từ App.js. Phần Text đầu tiên hiển thị tên sản phẩm. Phần Text tiếp theo hiển thị giá sản phẩm và sử dụng toLocaleString('vi-VN') để định dạng số tiền theo cách hiển thị của Việt Nam. Phần Text tiếp theo hiển thị mô tả sản phẩm.

Phần button tạo một nút có nội dung "Xem sản phẩm". Trong phiên bản hiện tại, nút này chủ yếu dùng để trang trí giao diện và chưa thực hiện chức năng chuyển trang hoặc mua sản phẩm.

Phần StyleSheet.create() chứa các thuộc tính giao diện của ProductCard như kích thước hình ảnh, màu sắc, kích thước chữ, khoảng cách, bo góc, bóng đổ và màu nền. Phần này giúp mỗi sản phẩm được hiển thị dưới dạng một thẻ sản phẩm rõ ràng và đẹp mắt.

Cuối file có export default ProductCard, có nhiệm vụ cho phép component ProductCard được sử dụng ở các file khác. Trong ứng dụng này, ProductCard được import vào App.js và được sử dụng bên trong FlatList.

Nhờ việc tách ProductCard thành một component riêng, chương trình có cấu trúc rõ ràng, dễ quản lý, dễ chỉnh sửa và có thể tái sử dụng cho nhiều sản phẩm khác nhau.
``````
code
import React from 'react';

import {
  View,
  Text,
  Image,
  StyleSheet,
} from 'react-native';

const ProductCard = ({
  name,
  image,
  price,
  description,
}) => {
  return (
    <View style={styles.card}>

      <Image
        source={{ uri: image }}
        style={styles.image}
      />

      <View style={styles.info}>

        <Text
          style={styles.name}
          numberOfLines={2}
        >
          {name}
        </Text>

        <Text style={styles.price}>
          {price.toLocaleString('vi-VN')} VNĐ
        </Text>

        <Text
          style={styles.description}
          numberOfLines={3}
        >
          {description}
        </Text>

        <View style={styles.button}>
          <Text style={styles.buttonText}>
            Xem sản phẩm
          </Text>
        </View>

      </View>

    </View>
  );
};

const styles = StyleSheet.create({
  card: {
    backgroundColor: '#ffffff',
    borderRadius: 15,
    marginBottom: 15,
    padding: 12,

    flexDirection: 'row',

    shadowColor: '#000000',
    shadowOffset: {
      width: 0,
      height: 2,
    },

    shadowOpacity: 0.15,
    shadowRadius: 4,

    elevation: 4,
  },

  image: {
    width: 110,
    height: 150,
    borderRadius: 10,
    backgroundColor: '#eeeeee',
  },

  info: {
    flex: 1,
    marginLeft: 15,
    justifyContent: 'center',
  },

  name: {
    fontSize: 18,
    fontWeight: 'bold',
    color: '#222222',
    marginBottom: 7,
  },

  price: {
    fontSize: 17,
    fontWeight: 'bold',
    color: '#e53935',
    marginBottom: 7,
  },

  description: {
    fontSize: 14,
    color: '#666666',
    lineHeight: 19,
    marginBottom: 10,
  },

  button: {
    backgroundColor: '#222222',
    borderRadius: 8,
    paddingVertical: 7,
    paddingHorizontal: 10,
    alignSelf: 'flex-start',
  },

  buttonText: {
    color: '#ffffff',
    fontSize: 13,
    fontWeight: 'bold',
  },
});

export default ProductCard;

```````
Kết quả sau cùng :

<img width="331" height="617" alt="image" src="https://github.com/user-attachments/assets/e92aed49-0e4f-410d-878d-395324cd56a5" />

