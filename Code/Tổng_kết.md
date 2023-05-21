# TỔNG KẾT THU HOẠCH #

### Đề bài ###
- Tạo 10 bộ dữ liệu ngẫu nhiên, mỗi bộ có khoảng 10^6 giá trị.
- Cài đặt cây AVL và cây Đỏ-Đen.
- Chạy thử việc tạo cây bằng cách thêm lần lượt các số bộ dữ liệu đã tạo.
- Ghi nhận chiều cao cây, vẽ biểu đồ so sánh các chiều cao cây và giá trị logN, 1.45logN. 
- Viết báo cáo thực nghiệm.

## 1. Cây AVL ##
#### a) Thông tin cơ bản ####
- Cây AVL là cây nhị phân tìm kiếm (BST) tự cân bằng, mà ở đó, độ khác biệt ``` chiều cao ``` giữa cây con trái và phải không quá 1 cho tất cả các node.
- Chiều cao tối đa $log_2(n)$ 
#### b) Vì sao nên xài cây AVL ####
- Nếu chỉ xài cây nhị phan tìm kiếm bình thường thì độ phức tạp là $O(n)$.
- Nếu xài cây AVL, thì độ phức tạp sẽ được giảm xuống còn $O(log_2(n))$.
#### c) Các trường hợp mất cân bằng ####
- Cây AVL có các chức năng như ``` chèn, xóa, cân bằng lại ```.
- Khi chèn 1 Node mới vào cây, nếu mất cân bằng sẽ xảy ra các trường hợp sau:
  - Left left case:
  ![image](https://github.com/PeanutButter6996/IT003/assets/109911533/76499384-406a-471c-9225-5ad69ec1daa4)
  
  - Right right case:
  ![image](https://github.com/PeanutButter6996/IT003/assets/109911533/81c7fcb8-f27e-480b-9a6b-ffc8702fdc1b)
  
  - Left right case:
  ![image](https://github.com/PeanutButter6996/IT003/assets/109911533/e7b91d99-5b38-47fe-b06a-819300a0465e)

  - Right left case:
  ![image](https://github.com/PeanutButter6996/IT003/assets/109911533/48d39a63-4114-4282-9ee4-aa3c64cf6fdf)

#### d) Giải pháp ####
- Với các trường hợp chỉ lệch trái hay phải, ta thực hiện 1 phép quay phải (đối với lệch trái) và quay trái (đối với lệch phải)
  - Left left case:
  ![image](https://github.com/PeanutButter6996/IT003/assets/109911533/ee1c3b7c-a782-4572-9c51-8428ddcbb12a)
  ```cpp
  //Right rotation to balance
  if (balance > 1 && data < node->left->data)
        return rightRotate(node);
  ```
  
  - Right right case:
    - Ngược lại của left left case.
  ```cpp
  // Left rotation to balance
  if (balance < -1 && data > node->right->data)
        return leftRotate(node);
  ```
  
- Với các trường hợp còn lại là ``` Left right case ```, hay ```Right left case```, thì cần thực hiện xoáy kép để đưa về cân bằng
  - Left right case :
  ![image](https://github.com/PeanutButter6996/IT003/assets/109911533/717bb77e-997b-4f83-8df3-24f2b4810488)
  ```cpp
  if (balance > 1 && data > node->left->data)
    {
        node->left = leftRotate(node->left);
        return rightRotate(node);
    }
  ```

  - Right left case:
    - Ngược lại của left right case
  ```cpp
   if (balance < -1 && data < node->right->data)
    {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }
   ```
 
## 2. Cây đỏ đen ##
#### a) Thông tin cơ bản ####
