**TRƯỜNG ĐẠI HỌC CÔNG NGHỆ SÀI GÒN**

KHOA CÔNG NGHỆ THÔNG TIN

**BÀI TẬP NHÓM GIỮA KỲ MÔN**
**TRIỂN KHAI DỰ ÁN THÔNG TIN**

***Giáo viên hướng dẫn:*** **Ths. Nguyễn Lạc An Thư**

***Sinh viên thực hiện:***

| STT | MSSV | Họ tên | Lớp | Điểm thi |
| :---: | :---: | :---: | :---: | :---: |
| 1 |  |  |  |  |
| 2 |  |  |  |  |
| 3 |  |  |  |  |
| 4 |  |  |  |  |
| 5 |  |  |  |  |

Tp.Hồ Chí Minh, tháng 03/2017

1. **Bảng phân công nhiệm vụ:**

| STT | Họ tên | Nhiệm vụ  |
| :---- | :---- | :---- |
| 1 |  |  |

2. **Mục Lục**

[**1. NỘI DUNG TÌM HIỂU CÁC RBTV TRONG OPENERP: 3**](#1-nội-dung-tìm-hiểu-các-rbtv-trong-openerp-thực-hành-buổi-2)

[**1.1. RBTV 1: Ràng buộc tính hợp lệ của dữ liệu (Giá, Ngày tháng)**](#11-rbtv-1-ràng-buộc-tính-hợp-lệ-của-dữ-liệu)

[a. Nội dung của ràng buộc toàn vẹn:](#1-nội-dung-của-ràng-buộc-toàn-vẹn)

[b. Quy trình kiểm tra RBTV1:](#2-quy-trình-kiểm-tra-rbtv1)

[**1.2. RBTV 2: Ràng buộc duy nhất (Unique)**](#12-rbtv-2-ràng-buộc-duy-nhất)

[**1.3. RBTV 3: Ràng buộc khóa ngoại (Restrict Delete)**](#13-rbtv-3-ràng-buộc-tham-chiếu-xóa)

[**2. XÂY DỰNG CHỨC NĂNG QUẢN LÝ GAME: 3**](#2-xây-dựng-chức-năng-quản-lý-game)

[**2.1. Mô tả nghiệp vụ(ghi rõ RBTV)**](#21-mô-tả-nghiệp-vụ)

[**2.2. Thiết kế Giao diện**](#22-thiết-kế-giao-diện)

[**2.3. Cài đặt (sourcecode)**](#23-cài-đặt-sourcecode)


1. # **Nội dung tìm hiểu các RBTV trong OpenERP (Thực hành buổi 2):**

   1. ## ***RBTV 1: Ràng buộc tính hợp lệ của dữ liệu***

      1. ### Nội dung của ràng buộc toàn vẹn:
         Hệ thống Quản lý Game áp dụng các quy chuẩn kiểm tra tính hợp lệ chặt chẽ đối với toàn bộ các đối tượng dữ liệu trước khi lưu trữ vào cơ sở dữ liệu:

         - **Trò chơi (Game):**
           - **Tên trò chơi:** Bắt buộc phải nhập, không được phép để trống và không được chứa toàn khoảng trắng.
           - **Ngày phát hành và Trạng thái:** Ngày phát hành bắt buộc phải nhập và không được để trống. Đồng thời phải phù hợp với trạng thái phát triển:
             - Trò chơi ở trạng thái **Đã phát hành** phải có Ngày phát hành nhỏ hơn hoặc bằng ngày giờ hiện tại.
             - Trò chơi ở trạng thái **Sắp phát hành** phải có Ngày phát hành lớn hơn ngày giờ hiện tại.
           - **Giá bán và Trạng thái kinh doanh:**
             - Trò chơi được đánh dấu là **Miễn phí** thì giá bán bắt buộc phải bằng 0.
             - Trò chơi **Không miễn phí (Trả phí)** thì giá bán bắt buộc phải lớn hơn 0.
             - Trò chơi ở trạng thái **Đã hủy** bắt buộc phải có giá bán bằng 0 (chặn hoàn toàn việc bán sản phẩm đã hủy).
           - **Dữ liệu bắt buộc liên quan:** Khi tạo mới trò chơi, bắt buộc phải cung cấp thông tin về Nhà phát hành, Studio phát triển game, danh sách các Thể loại và các Nền tảng chơi game.
           - **Ràng buộc sau khi phát hành:** Không cho phép thay đổi Nhà phát hành, Studio phát triển, Series (Chuỗi game) hoặc danh sách các Thể loại sau khi trò chơi đã chuyển sang trạng thái **Đã phát hành** nhằm bảo vệ tính nhất quán lịch sử sản phẩm.

         - **Phiên bản game (Version):**
           - **Tên phiên bản:** Bắt buộc phải nhập, không được để trống, và bắt buộc phải tuân theo định dạng chuẩn Semantic Versioning là `MAJOR.MINOR.PATCH` (ví dụ: `1.0.0`, `1.2.4`, `10.0.0`). Các định dạng phi tiêu chuẩn đều bị chặn.
           - **Nội dung cập nhật:** Bắt buộc phải nhập chi tiết nhật ký thay đổi của phiên bản.
           - **Trạng thái trò chơi liên kết:** Chỉ cho phép tạo mới hoặc chỉnh sửa phiên bản cho những trò chơi đã được **Đã phát hành**. Các trò chơi ở trạng thái nháp hay đang phát triển đều không được phép thêm phiên bản.
           - **Thứ tự số phiên bản:** Phiên bản mới được tạo phải có số phiên bản lớn hơn tất cả số phiên bản hiện có của trò chơi đó (áp dụng thuật toán so sánh phân rã tuple số học chuẩn xác).

         - **Studio phát triển game:**
           - **Tên studio:** Bắt buộc phải nhập và không được để trống.
           - **Trụ sở chính:** Bắt buộc phải nhập thông tin địa điểm trụ sở.
           - **Nhân sự tối thiểu:** Mỗi studio khi lưu trữ bắt buộc phải có ít nhất một nhân viên trực thuộc.

         - **Nhà phát hành (Publisher):**
           - **Tên nhà phát hành:** Bắt buộc phải nhập và không được để trống.
           - **Quốc gia:** Bắt buộc phải nhập quốc gia đặt trụ sở.

         - **Nhân viên (Member):**
           - **Tên nhân viên:** Bắt buộc phải nhập và không được để trống.
           - **Vai trò/Chức vụ:** Bắt buộc phải chỉ định ít nhất một vai trò công việc cho nhân viên.

         - **Thể loại game, Nền tảng chơi game, Series game, và Vai trò của nhân viên:**
           - Bắt buộc phải có thông tin tên danh mục, không được để trống.

      2. ### Quy trình kiểm tra RBTV1:
         - Quá trình xác thực diễn ra hoàn toàn tự động ở cả hai thao tác: tạo mới dữ liệu và cập nhật dữ liệu của mọi đối tượng trong hệ thống.
         - Nếu bất kỳ dữ liệu nào vi phạm các quy tắc trên, hệ thống sẽ ngay lập tức chặn thao tác và hiển thị hộp thoại thông báo lỗi chi tiết bằng tiếng Việt để người dùng điều chỉnh.

#### Chụp lại màn hình kết quả và diễn giải kết quả đó. {#chụp-lại-màn-hình-kết-quả-và-diễn-giải-kết-quả-đó.}
*(Sinh viên tự bổ sung ảnh chụp màn hình)*

   2. ## ***RBTV 2: Ràng buộc duy nhất***
      1. ### Nội dung của ràng buộc toàn vẹn:
         Để đảm bảo tính toàn vẹn và tránh trùng lặp thông tin danh mục, hệ thống kiểm soát chặt chẽ tính duy nhất cho các trường định danh tên của toàn bộ các đối tượng dữ liệu trong cơ sở dữ liệu:
         - **Tên trò chơi (Game):** Tên của mỗi tựa game khi đăng ký bắt buộc phải là duy nhất trong toàn bộ hệ thống trò chơi. Ràng buộc này ngăn chặn tuyệt đối việc tạo hai trò chơi có tên hoàn toàn giống nhau, tránh sai lệch và trùng lặp danh mục.
         - **Tên phiên bản (Version):** Số hiệu phiên bản (ví dụ: `1.0.0`) bắt buộc phải là duy nhất trong phạm vi của cùng một trò chơi cụ thể. Hệ thống cho phép các trò chơi khác nhau có cùng số hiệu phiên bản, nhưng cấm tuyệt đối một trò chơi có hai phiên bản trùng số hiệu.
         - **Tên Nhà phát hành (Publisher):** Tên của các tổ chức phát hành bắt buộc phải là duy nhất trên toàn bộ hệ thống. Tránh việc tạo trùng lặp thông tin đối tác phân phối game.
         - **Tên Studio phát triển game (Studio):** Tên của các studio phát triển game không được phép trùng lặp. Điều này đảm bảo tính định danh chính xác về thương hiệu của đơn vị sản xuất trò chơi.
         - **Tên Nhân viên (Member):** Tên của mỗi nhân sự trong hệ thống nhân sự phát triển game bắt buộc phải là duy nhất để phục vụ công tác quản lý phân công công việc, chức vụ và thành viên studio một cách chuẩn xác, không bị nhầm lẫn.
         - **Tên Thể loại game (Genre):** Tên của mỗi thể loại game (ví dụ: RPG, Action, Adventure) bắt buộc phải là duy nhất trên toàn bộ danh mục thể loại của hệ thống, giúp quy trình phân loại game luôn khoa học và nhất quán.
         - **Tên Nền tảng chơi game (Platform):** Tên gọi của các nền tảng chơi game (ví dụ: PC, PS5, Android) bắt buộc phải là duy nhất để hệ thống quản lý danh sách thiết bị phát hành một cách chính xác.
         - **Tên Series game (Series):** Tên của mỗi series/chuỗi trò chơi bắt buộc phải là duy nhất trong cơ sở dữ liệu để định danh chính xác các dòng thương hiệu game cốt truyện liền mạch.
         - **Tên Vai trò/Chức vụ nhân viên (Role):** Tên của các chức danh công việc trong đội ngũ phát triển (ví dụ: Game Director, Programmer, Artist) bắt buộc phải là duy nhất để phân định rõ ràng trách nhiệm công việc của từng nhân sự.

      2. ### Quy trình kiểm tra RBTV2:
         - Khi người dùng thực hiện tạo mới hoặc đổi tên một bản ghi, hệ thống sẽ tự động quét cơ sở dữ liệu để kiểm tra sự tồn tại của tên đó.
         - Nếu phát hiện đã tồn tại một bản ghi trùng tên (không tính chính bản ghi đang chỉnh sửa), hệ thống sẽ từ chối lưu và đưa ra cảnh báo trùng lặp cụ thể.

#### Chụp lại màn hình kết quả và diễn giải kết quả đó.
*(Sinh viên tự bổ sung ảnh chụp màn hình)*

   3. ## ***RBTV 3: Ràng buộc tham chiếu xóa (Restrict Delete)***
      1. ### Nội dung của ràng buộc toàn vẹn:
         Hệ thống thiết lập cơ chế khóa an toàn cấp cao nhằm ngăn chặn việc xóa các dữ liệu cốt lõi đang được sử dụng ở các bảng khác:
         - **Trò chơi:** Không thể xóa trò chơi nếu trò chơi đó đang có dữ liệu **Phiên bản** được liên kết.
         - **Nhà phát hành:** Không thể xóa Nhà phát hành nếu vẫn đang có các **Trò chơi** thuộc nhà phát hành này.
         - **Studio phát triển:** Không thể xóa Studio nếu studio đó vẫn đang phát triển ít nhất một **Trò chơi** hoặc đang có **Nhân viên** thuộc studio đó quản lý.
         - **Nhân viên:** Không thể xóa Nhân viên nếu nhân viên đó vẫn đang trực thuộc làm việc tại một **Studio** hoặc đang được chỉ định các **Vai trò/Chức vụ** phát triển.
         - **Thể loại game:** Không thể xóa Thể loại game nếu vẫn còn **Trò chơi** thuộc thể loại này.
         - **Nền tảng chơi game:** Không thể xóa Nền tảng chơi game nếu vẫn còn **Trò chơi** được phát hành trên nền tảng đó.
         - **Series game:** Không thể xóa Series game nếu vẫn còn **Trò chơi** thuộc chuỗi series đó.
         - **Vai trò/Chức vụ:** Không thể xóa Vai trò nếu vai trò này vẫn đang được gán cho ít nhất một **Nhân viên**.

      2. ### Quy trình kiểm tra RBTV3:
         - Bất cứ khi nào thao tác xóa được yêu cầu trên bất kỳ thực thể nào, hệ thống sẽ thực hiện kiểm tra khóa ngoại chéo trên toàn bộ cơ sở dữ liệu.
         - Nếu có bất kỳ liên kết tham chiếu nào còn hoạt động, thao tác xóa sẽ bị ngăn chặn triệt để, đảm bảo cơ sở dữ liệu không bao giờ xảy ra lỗi liên kết rác hoặc mất an toàn dữ liệu.

#### Chụp lại màn hình kết quả và diễn giải kết quả đó.
*(Sinh viên tự bổ sung ảnh chụp màn hình)*


2. # **Xây dựng chức năng quản lý danh mục Game:**

   1. ## ***Mô tả nghiệp vụ(ghi rõ RBTV)*** {#mô-tả-nghiệp-vụ-ghi-rõ-rbtv}
      Hệ thống nhằm mục đích quản lý toàn diện thông tin của các tựa Game, Tổ chức phát hành và Nhân sự tham gia phát triển.
      Các đối tượng chính bao gồm:
      - **Game:** Quản lý thông tin chung (Tên, Giá, Ngày phát hành, Trạng thái), các đối tượng liên quan (Thể loại, Nền tảng, Series) và các Phiên bản (Version) của game đó. Ràng buộc: Mỗi game thuộc về 1 Studio, 1 Nhà phát hành, 1 Series. Có thể thuộc nhiều Thể loại và Nền tảng (Quan hệ n-n).
      - **Tổ chức & Nhân sự:** Quản lý Nhà phát hành (Publisher), Studio phát triển, Nhân viên (Member), và Vai trò (Role). Ràng buộc: Một Studio có thể có nhiều Nhân viên (n-n), một nhân viên có nhiều Vai trò (n-n).
      - **RBTV trên Form/Nghiệp vụ:**
        - Khi tạo game, bắt buộc phải nhập đủ các thông tin: tên game, nhà phát hành, studio phát triển, ngày phát hành, trạng thái, thể loại và nền tảng chơi.
        - Nếu game là miễn phí thì giá phải bằng 0; nếu không miễn phí thì giá phải lớn hơn 0.
        - Ngày phát hành phải phù hợp với trạng thái: game đã phát hành phải có ngày phát hành trong quá khứ hoặc hôm nay, game sắp phát hành phải có ngày sau hôm nay.
        - Không được thay đổi nhà phát hành, studio, series hoặc thể loại của game sau khi game đã ở trạng thái đã phát hành.
        - Tên của game, nhà phát hành, studio, nhân viên, thể loại, nền tảng, series và vai trò đều phải được nhập và không được trùng nhau.
        - Không được xóa Nhà phát hành nếu vẫn còn Game thuộc Nhà phát hành đó.
        - Không được xóa Studio nếu vẫn còn Game hoặc Nhân viên thuộc Studio đó.
        - Không được xóa Nhân viên nếu vẫn còn liên kết với Studio hoặc Vai trò.
        - Không được xóa Thể loại, Nền tảng, Series hoặc Vai trò khi chúng đang được sử dụng.
        - Phiên bản game chỉ được tạo hoặc cập nhật khi game liên kết đã được phát hành.
        - Tên phiên bản phải theo định dạng MAJOR.MINOR.PATCH, không được để trống, phải là duy nhất trong cùng một game và phải lớn hơn phiên bản đã tồn tại.
        - Khi có phiên bản mới hơn phiên bản hiện tại, hệ thống sẽ đánh dấu game có bản cập nhật và cho phép cập nhật.

   2. ## ***Thiết kế Giao diện:*** {#thiết-kế-giao-diện}
      - **Hệ thống Menu chính:**
        - Menu "Quản lý Game" với các chức năng con: "Games" (Danh sách game, Phiên bản, Series, Thể loại, Nền tảng) và "Tổ chức & Nhân sự" (Nhà phát hành, Studio phát triển game, Nhân viên, Vai tro).
      - **Tree View (Danh sách):**
        - Hiển thị theo dạng bảng với các cột quan trọng. Hỗ trợ tính năng `editable="bottom"` cho Thể loại, Nền tảng, Nhà phát hành để người dùng thao tác nhanh.
      - **Form View (Biểu mẫu):**
        - Chia theo nhóm (`<group>`) giúp người dùng dễ đọc. Sử dụng thẻ `<notebook>` với các tab (Mô tả, Chi tiết) để quản lý nội dung dài. Ở form Studio có tab quản lý trực tiếp danh sách Nhân viên.
      - **Search View (Tìm kiếm - Lọc):**
        - Tích hợp ô tìm kiếm theo nhiều tiêu chí (Tên game, Studio, Series, Giá...). Cung cấp các bộ lọc nâng cao như: Lọc Game tạo/phát hành từ hôm nay, lọc theo trạng thái (Đã phát hành, sắp phát hành, hủy). Có tính năng "Group by" (Nhóm theo) Studio, Series, Nhà phát hành.

   3. ## ***Cài đặt (sourcecode):***
      Các tính năng đã được lập trình chi tiết thông qua Model (`game.py`), View (`game_view.xml`) và Menu (`game_menu.xml`) theo chuẩn kiến trúc MVC của nền tảng OpenERP 7.0.

      ### 3.1 Lớp dữ liệu (Model) - File `game.py`
      Lớp Model chịu trách nhiệm định nghĩa toàn bộ cấu trúc các bảng trong cơ sở dữ liệu, mối quan hệ giữa các thực thể và các ràng buộc logic, kiểm tra nghiệp vụ tự động thông qua các hàm xử lý tạo mới (`create`), cập nhật (`write`) và ngăn chặn xóa dữ liệu vi phạm toàn vẹn khóa ngoại (`unlink`).

      ```python
      # -*- coding: utf-8 -*-
      from datetime import datetime
      import logging
      from openerp.osv import fields, osv

      try:
          integer_types = (int, long)
      except NameError:
          integer_types = (int,)

      _logger = logging.getLogger(__name__)


      def _as_list(ids):
          if isinstance(ids, integer_types):
              return [ids]
          return list(ids)


      def _has_model_reference(pool, cr, uid, model_name, field_name, ids, context=None):
          return bool(pool.get(model_name).search(
              cr,
              uid,
              [(field_name, 'in', _as_list(ids))],
              limit=1,
              context=context
          ))


      def _has_relation_reference(cr, table_name, column_name, ids):
          cr.execute(
              'SELECT 1 FROM %s WHERE %s = ANY(%%s) LIMIT 1' % (table_name, column_name),
              (_as_list(ids),)
          )
          return bool(cr.fetchone())


      def _raise_delete_restricted(record_name):
          raise osv.except_osv(
              u'Lỗi',
              u'Không thể xóa %s vì đang được sử dụng bởi dữ liệu khóa ngoại!' % record_name
          )

      class Game(osv.osv):
          """
          GAME MODEL - Core entity for video game information
          """

          _name = 'game.game'
          _log_access = True

          def unlink(self, cr, uid, ids, context=None):
              if _has_model_reference(self.pool, cr, uid, 'game.version', 'game_id', ids, context=context):
                  _raise_delete_restricted(u'game')
              return super(Game, self).unlink(cr, uid, ids, context=context)

          def _validate_release_date_status(self, status, release_date):
              """
              Validate release date against status rules.
              - released -> date must be today or in the past
              - upcoming -> date must be in the future
              - cancelled -> no restriction
              """
              if release_date is False or release_date is None:
                  raise osv.except_osv(
                      u'Lỗi',
                      u'Ngày phát hành không được để trống!'
                  )

              release_date = datetime.strptime(release_date, '%Y-%m-%d %H:%M:%S')
              now = datetime.now()

              if status == 'released' and release_date > now:
                  raise osv.except_osv(
                      u'Lỗi',
                      u'Game đã phát hành phải có ngày phát hành trước hoặc bằng ngày hiện tại!'
                  )

              if status == 'upcoming' and release_date <= now:
                  raise osv.except_osv(
                      u'Lỗi',
                      u'Game sắp phát hành phải có ngày phát hành sau ngày hiện tại!'
                  )

          def _validate_price_logic(self, cr, uid, ids, vals, context=None):
              """
              Enforce game price business rules based on the free flag.
              - if is_free is True: price must be 0
              - otherwise: price must be greater than 0
              """
              current_price = None
              current_is_free = False

              if ids:
                  record = self.browse(cr, uid, ids[0], context=context)
                  current_price = record.price
                  current_is_free = record.is_free

              is_free = vals.get('is_free', current_is_free)
              price = vals.get('price', current_price)

              if is_free:
                  if price is not None and price != 0:
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Game miễn phí phải có giá bằng 0!'
                      )
              else:
                  if price is None or price <= 0:
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Game không miễn phí phải có giá lớn hơn 0!'
                      )

          def _validate_unique_name(self, cr, uid, vals, exclude_ids=None, context=None):
              """
              Validate game name field and prevent duplicate names.
              """
              if 'name' not in vals:
                  return

              vals['name'] = vals['name'].strip()
              if vals['name'] == '':
                  raise osv.except_osv(
                      u'Lỗi',
                      u'Tên game không được để trống!'
                  )

              domain = [('name', '=', vals['name'])]
              if exclude_ids:
                  domain.append(('id', 'not in', exclude_ids))

              existing = self.search(
                  cr,
                  uid,
                  domain,
                  context=context
              )
              if existing:
                  raise osv.except_osv(
                      u'Lỗi',
                      u'Tên game đã tồn tại!'
                  )

          def create(self, cr, uid, vals, context=None):
              _logger.info('game.game create: uid=%s vals=%s', uid, vals)
              if 'publisher_id' not in vals:
                  raise osv.except_osv(
                      u'Lỗi',
                      u'Nhà phát hành không được để trống!'
                  )

              if 'studio_id' not in vals:
                  raise osv.except_osv(
                      u'Lỗi',
                      u'Studio phát triển game không được để trống!'
                  )

              if 'release_date' not in vals:
                  raise osv.except_osv(
                      u'Lỗi',
                      u'Ngày phát hành không được để trống!'
                  )

              self._validate_price_logic(cr, uid, None, vals, context=context)

              status = vals.get('status')
              if status and 'release_date' in vals:
                  self._validate_release_date_status(status, vals['release_date'])

              self._validate_unique_name(
                  cr,
                  uid,
                  vals,
                  exclude_ids=None,
                  context=context
              )

              return super(Game, self).create(cr, uid, vals, context=context)

          def write(self, cr, uid, ids, vals, context=None):
              _logger.info('game.game write: uid=%s ids=%s vals=%s', uid, ids, vals)
              game = self.browse(cr, uid, ids[0], context=context)
              current_status = game.status
              new_status = vals.get('status', current_status)
              new_release_date = vals.get('release_date', game.release_date)

              if 'release_date' in vals or 'status' in vals:
                  self._validate_release_date_status(new_status, new_release_date)

              # Prevent important business fields from changing after release.
              if current_status == 'released' and any(key in vals for key in ('studio_id', 'publisher_id', 'series_id', 'genres')):
                  raise osv.except_osv(
                      u'Lỗi',
                      u'Không thể thay đổi Nhà phát hành, Studio, Series hoặc Thể loại sau khi game đã phát hành!'
                  )

              self._validate_price_logic(cr, uid, ids, vals, context=context)

              self._validate_unique_name(
                  cr,
                  uid,
                  vals,
                  exclude_ids=ids,
                  context=context
              )

              return super(Game, self).write(cr, uid, ids, vals, context=context)

          def _get_version_display(self, cr, uid, ids, field_name, arg, context=None):
              result = {}
              records = self.browse(cr, uid, ids, context=context)
              for game in records:
                  if game.version_id:
                      result[game.id] = ", ".join([v.version_name for v in game.version_id])
                  else:
                      result[game.id] = 'Chưa có thông tin về phiên bản game'
              return result

          def _get_genres_display(self, cr, uid, ids, field_name, arg, context=None):
              result = {}
              records = self.browse(cr, uid, ids, context=context)
              for game in records:
                  if game.genres:
                      result[game.id] = ", ".join([g.name for g in game.genres])
                  else:
                      result[game.id] = 'Chưa có thông tin về thể loại game'
              return result

          def _get_publisher_display(self, cr, uid, ids, field_name, arg, context=None):
              result = {}
              records = self.browse(cr, uid, ids, context=context)
              for game in records:
                  if game.publisher_id:
                      result[game.id] = game.publisher_id.name
                  else:
                      result[game.id] = 'Chưa có thông tin về nhà phát hành'
              return result

          def _get_studio_display(self, cr, uid, ids, field_name, arg, context=None):
              result = {}
              records = self.browse(cr, uid, ids, context=context)
              for game in records:
                  if game.studio_id:
                      result[game.id] = game.studio_id.name
                  else:
                      result[game.id] = 'Chưa có thông tin về studio phát triển game'
              return result

          def _version_tuple(self, version):
              return tuple(map(int, version.split('.')))

          def _has_update(self, cr, uid, ids, field_name, arg, context=None):
              result = {}
              version_obj = self.pool.get('game.version')
              for game in self.browse(cr, uid, ids, context=context):
                  result[game.id] = False
                  version_ids = version_obj.search(
                      cr,
                      uid,
                      [('game_id', '=', game.id)],
                      order='version_name desc',
                      limit=1
                  )

                  if not version_ids:
                      continue

                  latest_version = version_obj.browse(
                      cr,
                      uid,
                      version_ids[0],
                      context=context
                  )
                  if not game.current_version:
                      result[game.id] = True
                      continue

                  current = self._version_tuple(game.current_version)
                  latest = self._version_tuple(latest_version.version_name)

                  if current < latest:
                      result[game.id] = True

              return result

          def _get_latest_version_display(self, cr, uid, ids, field_name, arg, context=None):
              result = {}
              version_obj = self.pool.get('game.version')
              for game in self.browse(cr, uid, ids, context=context):
                  version_ids = version_obj.search(
                      cr,
                      uid,
                      [('game_id', '=', game.id)],
                      order='version_name desc',
                      limit=1
                  )

                  if not version_ids:
                      result[game.id] = u'Chưa có phiên bản'
                      continue

                  latest_version = version_obj.browse(
                      cr,
                      uid,
                      version_ids[0],
                      context=context
                  )

                  if game.has_update:
                      result[game.id] = u'Có bản cập nhật %s' % latest_version.version_name
                  else:
                      result[game.id] = u'Đã cập nhật bản mới nhất'

              return result

          def action_update_game(self, cr, uid, ids, context=None):
              game = self.browse(cr, uid, ids[0], context=context)
              version_obj = self.pool.get('game.version')
              version_ids = version_obj.search(
                  cr,
                  uid,
                  [('game_id', '=', game.id)],
                  order='version_name desc',
                  limit=1
              )

              if version_ids:
                  latest_version = version_obj.browse(
                      cr,
                      uid,
                      version_ids[0],
                      context=context
                  )
                  self.write(
                      cr,
                      uid,
                      ids,
                      {
                          'current_version': latest_version.version_name
                      },
                      context=context
                  )
              return True

          _columns = {
              'name': fields.char(
                  'Tên game',
                  size=25,
                  required=True,
              ),
              'description': fields.text('Mô tả'),
              'create_date': fields.datetime(
                  'Ngày Tạo',
                  readonly=True
              ),
              'write_date': fields.datetime(
                  'Ngày cập nhật',
                  readonly=True
              ),
              'release_date': fields.datetime('Ngày phát hành'),
              'status': fields.selection([
                  ('released', 'Đã phát hành'),
                  ('upcoming', 'Sắp phát hành'),
                  ('cancelled', 'Đã hủy')
              ], 'Trạng thái', required=True),
              'notes': fields.text('Chi tiết'),
              'price': fields.float('Giá'),
              'is_free': fields.boolean('Miễn phí'),
              'publisher_id': fields.many2one(
                  'game.publisher',
                  'Nhà phát hành'
              ),
              'version_id': fields.one2many(
                  'game.version',
                  'game_id',
                  'Phiên bản'
              ),
              'genres': fields.many2many(
                  'game.genre',
                  'game_genre_rel',
                  'game_id',
                  'genre_id',
                  'Thể loại',
                  required=True
              ),
              'studio_id': fields.many2one(
                  'game.studio',
                  'Studio phát triển game'
              ),
              'series_id': fields.many2one(
                  'game.series',
                  'Series'
              ),
              'platforms': fields.many2many(
                  'game.platform',
                  'game_platform_rel',
                  'game_id',
                  'platform_id',
                  'Nền tảng',
                  required=True
              ),
              'display_publisher_name': fields.function(
                  _get_publisher_display,
                  type='char',
                  string='Tên nhà phát hành'
              ),
              'display_studio_name': fields.function(
                  _get_studio_display,
                  type='char',
                  string='Tên Studio'
              ),
              'display_genres_name': fields.function(
                  _get_genres_display,
                  type='char',
                  string='Tên Thể Loại'
              ),
              'display_version_name': fields.function(
                  _get_version_display,
                  type='char',
                  string='Các phiên bản'
              ),
              'current_version': fields.char(
                  'Phiên bản hiện tại',
                  size=20
              ),
              'has_update': fields.function(
                  _has_update,
                  type='boolean',
                  string='Có bản cập nhật'
              ),
              'latest_version_display': fields.function(
                  _get_latest_version_display,
                  type='char',
                  string='Trạng thái cập nhật'
              ),
          }


      class Publisher(osv.osv):
          """
          PUBLISHER MODEL
          """
          _name = 'game.publisher'
          _log_access = True

          def unlink(self, cr, uid, ids, context=None):
              if _has_model_reference(self.pool, cr, uid, 'game.game', 'publisher_id', ids, context=context):
                  _raise_delete_restricted(u'nhà phát hành')
              return super(Publisher, self).unlink(cr, uid, ids, context=context)

          def create(self, cr, uid, vals, context=None):
              _logger.info('game.publisher create: uid=%s vals=%s', uid, vals)
              if 'name' in vals:
                  vals['name'] = vals['name'].strip()
                  if vals['name'] == '':
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên Nhà phát hành không được để trống!'
                      )
                  existing = self.search(
                      cr,
                      uid,
                      [('name', '=', vals['name'])],
                      context=context
                  )
                  if existing:
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên Nhà phát hành đã tồn tại!'
                      )
              return super(Publisher, self).create(cr, uid, vals, context=context)

          def write(self, cr, uid, ids, vals, context=None):
              _logger.info('game.publisher write: uid=%s ids=%s vals=%s', uid, ids, vals)
              if 'name' in vals:
                  vals['name'] = vals['name'].strip()
                  if vals['name'] == '':
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên Nhà phát hành không được để trống!'
                      )
                  existing = self.search(
                      cr,
                      uid,
                      [('name', '=', vals['name'])],
                      context=context
                  )
                  if existing:
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên Nhà phát hành đã tồn tại!'
                      )
              return super(Publisher, self).write(cr, uid, ids, vals, context=context)

          _columns = {
              'name': fields.char(
                  'Tên nhà phát hành',
                  size=25,
                  required=True
              ),
              'country': fields.char(
                  'Quốc gia',
                  size=25,
                  required=True
              ),
              'create_date': fields.datetime(
                  'Ngày Tạo',
                  readonly=True
              ),
              'write_date': fields.datetime(
                  'Ngày cập nhật',
                  readonly=True
              ),
          }


      class Studio(osv.osv):
          """
          STUDIO MODEL - Manages development studios
          """
          _name = 'game.studio'
          _log_access = True

          def unlink(self, cr, uid, ids, context=None):
              if _has_model_reference(self.pool, cr, uid, 'game.game', 'studio_id', ids, context=context):
                  _raise_delete_restricted(u'studio')
              if _has_relation_reference(cr, 'game_studio_member_rel', 'studio_id', ids):
                  _raise_delete_restricted(u'studio')
              return super(Studio, self).unlink(cr, uid, ids, context=context)

          def create(self, cr, uid, vals, context=None):
              _logger.info('game.studio create: uid=%s vals=%s', uid, vals)
              if 'name' in vals:
                  vals['name'] = vals['name'].strip()
                  if vals['name'] == '':
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên Studio phát triển game không được để trống!'
                      )
                  existing = self.search(
                      cr,
                      uid,
                      [('name', '=', vals['name'])],
                      context=context
                  )
                  if existing:
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên Studio phát triển game đã tồn tại!'
                      )
              return super(Studio, self).create(cr, uid, vals, context=context)

          def write(self, cr, uid, ids, vals, context=None):
              _logger.info('game.studio write: uid=%s ids=%s vals=%s', uid, ids, vals)
              if 'name' in vals:
                  vals['name'] = vals['name'].strip()
                  if vals['name'] == '':
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên Studio phát triển game không được để trống!'
                      )
                  existing = self.search(
                      cr,
                      uid,
                      [('name', '=', vals['name'])],
                      context=context
                  )
                  if existing:
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên Studio phát triển game đã tồn tại!'
                      )
              return super(Studio, self).write(cr, uid, ids, vals, context=context)

          _columns = {
              'name': fields.char(
                  'Tên studio phát triển game',
                  size=25,
                  required=True
              ),
              'headquarter': fields.char(
                  'Trụ sở chính',
                  size=25,
                  required=True
              ),
              'create_date': fields.datetime(
                  'Ngày Tạo',
                  readonly=True
              ),
              'write_date': fields.datetime(
                  'Ngày cập nhật',
                  readonly=True
              ),
              'members': fields.many2many(
                  'game.member',
                  'game_studio_member_rel',
                  'studio_id',
                  'member_id',
                  'Nhân viên',
                  required=True
              ),
          }

      class Member(osv.osv):
          """
          MEMBER MODEL - Manages development team members
          """
          _name = 'game.member'
          _log_access = True

          def unlink(self, cr, uid, ids, context=None):
              if _has_relation_reference(cr, 'game_studio_member_rel', 'member_id', ids):
                  _raise_delete_restricted(u'nhân viên')
              if _has_relation_reference(cr, 'game_member_role_rel', 'member_id', ids):
                  _raise_delete_restricted(u'nhân viên')
              return super(Member, self).unlink(cr, uid, ids, context=context)

          def _get_studios_display(self, cr, uid, ids, field_name, arg, context=None):
              result = {}
              records = self.browse(cr, uid, ids, context=context)
              for member in records:
                  if member.studios:
                      result[member.id] = ", ".join([s.name for s in member.studios])
                  else:
                      result[member.id] = 'Chưa có thông tin về studio phát triển game'
              return result

          def create(self, cr, uid, vals, context=None):
              _logger.info('game.member create: uid=%s vals=%s', uid, vals)
              if 'name' in vals:
                  vals['name'] = vals['name'].strip()
                  if vals['name'] == '':
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên Nhân viên không được để trống!'
                      )
                  existing = self.search(
                      cr,
                      uid,
                      [('name', '=', vals['name'])],
                      context=context
                  )
                  if existing:
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên Nhân viên đã tồn tại!'
                      )
              return super(Member, self).create(cr, uid, vals, context=context)

          def write(self, cr, uid, ids, vals, context=None):
              _logger.info('game.member write: uid=%s ids=%s vals=%s', uid, ids, vals)
              if 'name' in vals:
                  vals['name'] = vals['name'].strip()
                  if vals['name'] == '':
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên Nhân viên không được để trống!'
                      )
                  existing = self.search(
                      cr,
                      uid,
                      [('name', '=', vals['name'])],
                      context=context
                  )
                  if existing:
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên Nhân viên đã tồn tại!'
                      )
              return super(Member, self).write(cr, uid, ids, vals, context=context)

          _columns = {
              'name': fields.char(
                  'Tên nhân viên',
                  size=25,
                  required=True
              ),
              'studios': fields.many2many(
                  'game.studio',
                  'game_studio_member_rel',
                  'member_id',
                  'studio_id',
                  'Studio',
              ),
              'roles': fields.many2many(
                  'game.role',
                  'game_member_role_rel',
                  'member_id',
                  'role_id',
                  'Chức vụ',
                  required=True
              ),
              'create_date': fields.datetime(
                  'Ngày Tạo',
                  readonly=True
              ),
              'write_date': fields.datetime(
                  'Ngày cập nhật',
                  readonly=True
              ),
              'display_studios_name': fields.function(
                  _get_studios_display,
                  type='char',
                  string='Studio phát triển game',
                  store=False
              ),
          }


      class Genre(osv.osv):
          """
          GENRE MODEL - Manages game genre categories
          """
          _name = 'game.genre'
          _log_access = True

          def unlink(self, cr, uid, ids, context=None):
              if _has_relation_reference(cr, 'game_genre_rel', 'genre_id', ids):
                  _raise_delete_restricted(u'thể loại')
              return super(Genre, self).unlink(cr, uid, ids, context=context)

          def create(self, cr, uid, vals, context=None):
              _logger.info('game.genre create: uid=%s vals=%s', uid, vals)
              if 'name' in vals:
                  vals['name'] = vals['name'].strip()
                  if vals['name'] == '':
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên thể loại không được để trống!'
                      )
                  existing = self.search(
                      cr,
                      uid,
                      [('name', '=', vals['name'])],
                      context=context
                  )
                  if existing:
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên thể loại đã tồn tại!'
                      )
              return super(Genre, self).create(cr, uid, vals, context=context)

          def write(self, cr, uid, ids, vals, context=None):
              _logger.info('game.genre write: uid=%s ids=%s vals=%s', uid, ids, vals)
              if 'name' in vals:
                  vals['name'] = vals['name'].strip()
                  if vals['name'] == '':
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên thể loại không được để trống!'
                      )
                  existing = self.search(
                      cr,
                      uid,
                      [('name', '=', vals['name'])],
                      context=context
                  )
                  if existing:
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên thể loại đã tồn tại!'
                      )
              return super(Genre, self).write(cr, uid, ids, vals, context=context)

          _columns = {
              'name': fields.char(
                  'Tên thể loại',
                  size=25,
                  required=True
              ),
              'create_date': fields.datetime(
                  'Ngày Tạo',
                  readonly=True
              ),
              'write_date': fields.datetime(
                  'Ngày cập nhật',
                  readonly=True
              ),
          }


      class Platform(osv.osv):
          """
          PLATFORM MODEL - Manages gaming platforms/systems
          """
          _name = 'game.platform'
          _log_access = True

          def unlink(self, cr, uid, ids, context=None):
              if _has_relation_reference(cr, 'game_platform_rel', 'platform_id', ids):
                  _raise_delete_restricted(u'nền tảng')
              return super(Platform, self).unlink(cr, uid, ids, context=context)

          def create(self, cr, uid, vals, context=None):
              _logger.info('game.platform create: uid=%s vals=%s', uid, vals)
              if 'name' in vals:
                  vals['name'] = vals['name'].strip()
                  if vals['name'] == '':
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên nền tảng không được để trống!'
                      )
                  existing = self.search(
                      cr,
                      uid,
                      [('name', '=', vals['name'])],
                      context=context
                  )
                  if existing:
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên nền tảng đã tồn tại!'
                      )
              return super(Platform, self).create(cr, uid, vals, context=context)

          def write(self, cr, uid, ids, vals, context=None):
              _logger.info('game.platform write: uid=%s ids=%s vals=%s', uid, ids, vals)
              if 'name' in vals:
                  if vals['name'] == '':
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên nền tảng không được để trống!'
                      )
                  existing = self.search(
                      cr,
                      uid,
                      [('name', '=', vals['name'])],
                      context=context
                  )
                  if existing:
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên nền tảng đã tồn tại!'
                      )
              return super(Platform, self).write(cr, uid, ids, vals, context=context)

          _columns = {
              'name': fields.char(
                  'Tên máy tính',
                  size=25,
                  required=True
              ),
              'create_date': fields.datetime(
                  'Ngày Tạo',
                  readonly=True
              ),
              'write_date': fields.datetime(
                  'Ngày cập nhật',
                  readonly=True
              ),
          }


      class Series(osv.osv):
          """
          SERIES MODEL - Manages game series/franchises
          """
          _name = 'game.series'
          _log_access = True

          def unlink(self, cr, uid, ids, context=None):
              if _has_model_reference(self.pool, cr, uid, 'game.game', 'series_id', ids, context=context):
                  _raise_delete_restricted(u'series')
              return super(Series, self).unlink(cr, uid, ids, context=context)

          def create(self, cr, uid, vals, context=None):
              _logger.info('game.series create: uid=%s vals=%s', uid, vals)
              if 'name' in vals:
                  vals['name'] = vals['name'].strip()
                  if vals['name'] == '':
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên series không được để trống!'
                      )
                  existing = self.search(
                      cr,
                      uid,
                      [('name', '=', vals['name'])],
                      context=context
                  )
                  if existing:
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên series đã tồn tại!'
                      )
              return super(Series, self).create(cr, uid, vals, context=context)

          def write(self, cr, uid, ids, vals, context=None):
              _logger.info('game.series write: uid=%s ids=%s vals=%s', uid, ids, vals)
              if 'name' in vals:
                  vals['name'] = vals['name'].strip()
                  if vals['name'] == '':
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên series không được để trống!'
                      )
                  existing = self.search(
                      cr,
                      uid,
                      [('name', '=', vals['name'])],
                      context=context
                  )
                  if existing:
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên series đã tồn tại!'
                      )
              return super(Series, self).write(cr, uid, ids, vals, context=context)

          _columns = {
              'name': fields.char(
                  'Tên series',
                  size=25,
                  required=True
              ),
              'description': fields.text('Mô tả'),
              'create_date': fields.datetime(
                  'Ngày Tạo',
                  readonly=True
              ),
              'write_date': fields.datetime(
                  'Ngày cập nhật',
                  readonly=True
              ),
          }


      class Role(osv.osv):
          _name = 'game.role'
          _log_access = True

          def unlink(self, cr, uid, ids, context=None):
              if _has_relation_reference(cr, 'game_member_role_rel', 'role_id', ids):
                  _raise_delete_restricted(u'vai trò')
              return super(Role, self).unlink(cr, uid, ids, context=context)

          def create(self, cr, uid, vals, context=None):
              _logger.info('game.role create: uid=%s vals=%s', uid, vals)
              if 'name' in vals:
                  vals['name'] = vals['name'].strip()
                  if vals['name'] == '':
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên vai trò không được để trống!'
                      )
                  existing = self.search(
                      cr,
                      uid,
                      [('name', '=', vals['name'])],
                      context=context
                  )
                  if existing:
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên vai trò đã tồn tại!'
                      )
              return super(Role, self).create(cr, uid, vals, context=context)

          def write(self, cr, uid, ids, vals, context=None):
              _logger.info('game.role write: uid=%s ids=%s vals=%s', uid, ids, vals)
              if 'name' in vals:
                  vals['name'] = vals['name'].strip()
                  if vals['name'] == '':
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên vai trò không được để trống!'
                      )
                  existing = self.search(
                      cr,
                      uid,
                      [('name', '=', vals['name'])],
                      context=context
                  )
                  if existing:
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên vai trò đã tồn tại!'
                      )
              return super(Role, self).write(cr, uid, ids, vals, context=context)

          _columns = {
              'name': fields.char(
                  'Tên vai trò',
                  size=25,
                  required=True
              ),
              'create_date': fields.datetime(
                  'Ngày Tạo',
                  readonly=True
              ),
              'write_date': fields.datetime(
                  'Ngày cập nhật',
                  readonly=True
              ),
          }


      import re

      class GameVersion(osv.osv):
          _name = 'game.version'

          def _version_tuple(self, version):
              return tuple(map(int, version.split('.')))

          def _get_latest_version(self, cr, uid, game_id, exclude_ids=None, context=None):
              version_ids = self.search(
                  cr,
                  uid,
                  [('game_id', '=', game_id)] + ([('id', 'not in', exclude_ids)] if exclude_ids else []),
                  context=context
              )
              latest_version = None
              for version in self.browse(cr, uid, version_ids, context=context):
                  if latest_version is None or self._version_tuple(version.version_name) > self._version_tuple(latest_version.version_name):
                      latest_version = version
              return latest_version

          def create(self, cr, uid, vals, context=None):
              _logger.info('game.version create: uid=%s vals=%s', uid, vals)
              if 'version_name' in vals:
                  vals['version_name'] = vals['version_name'].strip()

                  if vals['version_name'] == '':
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên phiên bản không được để trống!'
                      )

                  if not re.match(r'^\d+\.\d+\.\d+$', vals['version_name']):
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên phiên bản phải có định dạng MAJOR.MINOR.PATCH!'
                      )

                  game_id = vals.get('game_id')
                  if not game_id:
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Phiên bản phải liên kết với một Game.'
                      )

                  game = self.pool.get('game.game').browse(cr, uid, game_id, context=context)
                  if game.status != 'released':
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Chỉ có thể tạo phiên bản cho game đã phát hành.'
                      )

                  existing = self.search(
                      cr,
                      uid,
                      [
                          ('version_name', '=', vals['version_name']),
                          ('game_id', '=', game_id)
                      ],
                      context=context
                  )

                  if existing:
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên phiên bản đã tồn tại!'
                      )

                  latest_version = self._get_latest_version(cr, uid, game_id, context=context)
                  if latest_version:
                      current = self._version_tuple(vals['version_name'])
                      latest = self._version_tuple(latest_version.version_name)
                      if current <= latest:
                          raise osv.except_osv(
                              u'Lỗi',
                              u'Số phiên bản phải lớn hơn phiên bản đã tồn tại!'
                          )

              return super(GameVersion, self).create(
                  cr,
                  uid,
                  vals,
                  context=context
              )

          def write(self, cr, uid, ids, vals, context=None):
              _logger.info('game.version write: uid=%s ids=%s vals=%s', uid, ids, vals)

              if 'version_name' in vals or 'game_id' in vals:
                  if 'version_name' in vals:
                      vals['version_name'] = vals['version_name'].strip()

                      if vals['version_name'] == '':
                          raise osv.except_osv(
                              u'Lỗi',
                              u'Tên phiên bản không được để trống!'
                          )

                      if not re.match(r'^\d+\.\d+\.\d+$', vals['version_name']):
                          raise osv.except_osv(
                              u'Lỗi',
                              u'Tên phiên bản phải có định dạng MAJOR.MINOR.PATCH!'
                          )

                  current_version = self.browse(
                      cr,
                      uid,
                      ids[0],
                      context=context
                  )

                  game_id = vals.get('game_id', current_version.game_id.id)
                  if not game_id:
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Phiên bản phải liên kết với một Game.'
                      )

                  game = self.pool.get('game.game').browse(cr, uid, game_id, context=context)
                  if game.status != 'released':
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Chỉ có thể cập nhật phiên bản cho game đã phát hành.'
                      )

                  existing = self.search(
                      cr,
                      uid,
                      [
                          ('version_name', '=', vals.get('version_name', current_version.version_name)),
                          ('game_id', '=', game_id),
                          ('id', 'not in', ids)
                      ],
                      context=context
                  )

                  if existing:
                      raise osv.except_osv(
                          u'Lỗi',
                          u'Tên phiên bản đã tồn tại!'
                      )

                  latest_version = self._get_latest_version(cr, uid, game_id, exclude_ids=ids, context=context)
                  if latest_version and 'version_name' in vals:
                      current = self._version_tuple(vals['version_name'])
                      latest = self._version_tuple(latest_version.version_name)
                      if current <= latest:
                          raise osv.except_osv(
                              u'Lỗi',
                              u'Số phiên bản phải lớn hơn phiên bản đã tồn tại!'
                          )

              return super(GameVersion, self).write(
                  cr,
                  uid,
                  ids,
                  vals,
                  context=context
              )

          _columns = {
              'version_name': fields.char(
                  'Phiên bản',
                  size=20,
                  required=True
              ),
              'enhancement_notes': fields.text(
                  'Nội dung cập nhật',
                  required=True
              ),
              'game_id': fields.many2one(
                  'game.game',
                  'Game',
                  ondelete='cascade'
              ),
              'create_date': fields.datetime(
                  'Ngày Tạo',
                  readonly=True
              ),
              'write_date': fields.datetime(
                  'Ngày cập nhật',
                  readonly=True
              ),
          }
      ```

      ### 3.2 Lớp giao diện (View) - File `game_view.xml`
      Lớp View định nghĩa cấu trúc giao diện và layout hiển thị trực quan cho người dùng cuối bao gồm các biểu mẫu nhập liệu (`form`), danh sách lưới (`tree`) và bộ lọc nâng cao (`search`).

      ```xml
      <?xml version="1.0" encoding="utf-8"?>
      <openerp>
          <data>
              <!-- GAME Tree View -->
              <record model="ir.ui.view" id="view_game_tree">
                  <field name="name">game.tree</field>
                  <field name="model">game.game</field>
                  <field name="type">tree</field>
                  <field name="arch" type="xml">
                      <tree string="Danh sách các tựa game">
                          <field name="name"/>
                          <field name="description"/>
                          <field name="genres"/>
                          <field name="platforms"/>
                          <field name="release_date"/>
                          <field name="status"/>
                          <field name="is_free"/>
                          <field name="price"/>
                          <field name="publisher_id"/>
                          <field name="studio_id"/>
                          <field name="series_id"/>
                          <field name="display_version_name"/>
                          <field name="current_version"/>
                          <field name="latest_version_display"/>
                          <field name="has_update" invisible="1"/>
                          <field name="notes"/>
                          <button
                              name="action_update_game"
                              string="Cập nhật"
                              type="object"
                              icon="gtk-refresh"
                              attrs="{'invisible':[('has_update','=',False)]}"
                          />
                          <field name="create_date"/>
                          <field name="write_date"/>
                      </tree>
                  </field>
              </record>

              <record model="ir.ui.view" id="view_game_form">
                  <field name="name">game.form</field>
                  <field name="model">game.game</field>
                  <field name="arch" type="xml">
                      <form string="Thông tin Game" version="7.0">
                          <sheet>
                              <group col="4">
                                  <field name="name" colspan="4" string="Tên game:"/>
                              </group>
                              <group col="2" string="Thông tin cơ bản">
                                  <field name="genres" string="Thể loại:"/>
                                  <field name="status" string="Trạng thái:"/>
                                  <field name="release_date" string="Ngày phát hành:"/>
                                  <field name="is_free" string="Miễn phí"/>
                                  <field name="price" string="Giá:"/>
                              </group>
                              <group col="2" string="Thông tin phát hành">
                                  <field name="publisher_id" string="Nhà phát hành:"/>
                                  <field name="studio_id" string="Studio phát triển game:"/>
                                  <field name="series_id" string="Series:"/>
                                  <field name="current_version" readonly="1" string="Phiên bản hiện tại:"/>
                                  <field name="latest_version_display" readonly="1" string="Trạng thái cập nhật:"/>
                              </group>
                              <group col="4">
                                  <field name="platforms" string="Nền tảng chơi:" colspan="4"/>
                              </group>
                              <group col="4">
                                  <field name="version_id" string="Phiên bản:"/>
                              </group>
                              <notebook>
                                  <page string="Mô tả">
                                      <field name="description" nolabel="1"/>
                                  </page>
                                  <page string="Chi tiết">
                                      <field name="notes" nolabel="1" placeholder="Thêm các chi tiết bổ sung về tựa game..."/>
                                  </page>
                              </notebook>
                          </sheet>
                      </form>
                  </field>
              </record>

              <!-- GAME Search View -->
              <record model="ir.ui.view" id="view_game_search">
                  <field name="name">game.search</field>
                  <field name="model">game.game</field>
                  <field name="type">search</field>
                  <field name="arch" type="xml">
                      <search string="Tìm kiếm game">
                          <group col="4" string="Tìm kiếm">
                              <field name="name" select="1" string="Tên game" filter_domain="[('name', 'ilike', self)]"/>
                              <field name="studio_id" select="1" string="Studio phát triển"/>
                              <field name="series_id" select="1" string="Series"/>
                              <field name="publisher_id" select="1" string="Nhà phát hành"/>
                              <field name="price" string="Giá" filter_domain="[('price', '>=', self)]"/>
                              <field name="create_date" string="Ngày tạo" filter_domain="[('create_date', '>=', self)]"/>
                              <field name="release_date" string="Ngày phát hành" filter_domain="[('release_date', '>=', self)]"/>
                          </group>
                          <separator/>
                          <filter string="Game tạo từ hôm nay"
                              name="create_date_today"
                              domain="[('create_date','>=', time.strftime('%%Y-%%m-%%d 00:00:00'))]"/>
                          <filter string="Game phát hành từ hôm nay"
                              name="release_date_today"
                              domain="[('release_date','>=', time.strftime('%%Y-%%m-%%d 00:00:00'))]"/>
                          <filter string="Đã phát hành" name="released" domain="[('status', '=', 'released')]"/>
                          <filter string="Sắp phát hành" name="upcoming" domain="[('status', '=', 'upcoming')]"/>
                          <filter string="Đã huỷ" name="cancelled" domain="[('status', '=', 'cancelled')]"/>
                          <group expand="0" string="Nhóm theo">
                              <filter string="Studio" name="group_studio" context="{'group_by': 'studio_id'}"/>
                              <filter string="Series" name="group_series" context="{'group_by': 'series_id'}"/>
                              <filter string="Nhà phát hành" name="group_publisher" context="{'group_by': 'publisher_id'}"/>
                          </group>
                      </search>
                  </field>
              </record>

              <!-- GAME Action -->
              <record model="ir.actions.act_window" id="action_game">
                  <field name="name">Thông tin Game</field>
                  <field name="res_model">game.game</field>
                  <field name="view_mode">tree,form</field>
                  <field name="search_view_id" ref="view_game_search"/>
              </record>

              <!-- PUBLISHER Tree View -->
              <record model="ir.ui.view" id="view_publisher_tree">
                  <field name="name">publisher.tree</field>
                  <field name="model">game.publisher</field>
                  <field name="type">tree</field>
                  <field name="arch" type="xml">
                      <tree string="Danh sách Nhà phát hành" editable="bottom">
                          <field name="name"/>
                          <field name="country"/>
                          <field name="create_date"/>
                          <field name="write_date"/>
                      </tree>
                  </field>
              </record>

              <!-- PUBLISHER Form View -->
              <record model="ir.ui.view" id="view_publisher_form">
                  <field name="name">publisher.form</field>
                  <field name="model">game.publisher</field>
                  <field name="arch" type="xml">
                      <form string="Nhà phát hành" version="7.0">
                          <header></header>
                          <sheet>
                              <group col="2" string="Thông tin nhà phát hành">
                                  <field name="name" string="Tên:"/>
                                  <field name="country" string="Quốc gia:"/>
                              </group>
                          </sheet>
                      </form>
                  </field>
              </record>

              <!-- PUBLISHER Action -->
              <record model="ir.actions.act_window" id="action_publisher">
                  <field name="name">Nhà phát hành</field>
                  <field name="res_model">game.publisher</field>
                  <field name="view_type">form</field>
                  <field name="view_mode">tree,form</field>
              </record>

              <!-- STUDIO Tree View -->
              <record model="ir.ui.view" id="view_studio_tree">
                  <field name="name">studio.tree</field>
                  <field name="model">game.studio</field>
                  <field name="type">tree</field>
                  <field name="arch" type="xml">
                      <tree string="Danh sách Studio phát triển game">
                          <field name="name"/>
                          <field name="headquarter"/>
                          <field name="create_date"/>
                          <field name="write_date"/>
                      </tree>
                  </field>
              </record>

              <!-- STUDIO Form View -->
              <record model="ir.ui.view" id="view_studio_form">
                  <field name="name">studio.form</field>
                  <field name="model">game.studio</field>
                  <field name="arch" type="xml">
                      <form string="Studio phát triển game" version="7.0">
                          <header></header>
                          <sheet>
                              <group col="2" string="Thông tin chung">
                                  <field name="name" string="Tên:"/>
                                  <field name="headquarter" string="Trụ sở chính:"/>
                              </group>
                              <notebook>
                                  <page string="Nhân viên">
                                      <field name="members">
                                          <tree string="Danh sách nhân viên" editable="bottom">
                                              <field name="name" string="Tên"/>
                                              <field name="roles" string="Vai trò"/>
                                          </tree>
                                      </field>
                                  </page>
                              </notebook>
                          </sheet>
                      </form>
                  </field>
              </record>

              <!-- STUDIO Action -->
              <record model="ir.actions.act_window" id="action_studio">
                  <field name="name">Studio phát triển game</field>
                  <field name="res_model">game.studio</field>
                  <field name="view_type">form</field>
                  <field name="view_mode">tree,form</field>
              </record>

              <!-- MEMBER Tree View -->
              <record model="ir.ui.view" id="view_member_tree">
                  <field name="name">member.tree</field>
                  <field name="model">game.member</field>
                  <field name="type">tree</field>
                  <field name="arch" type="xml">
                      <tree string="Danh sách nhân viên">
                          <field name="name"/>
                          <field name="roles"/>
                          <field name="display_studios_name"/>
                          <field name="create_date"/>
                          <field name="write_date"/>
                      </tree>
                  </field>
              </record>

              <!-- MEMBER Form View -->
              <record model="ir.ui.view" id="view_member_form">
                  <field name="name">member.form</field>
                  <field name="model">game.member</field>
                  <field name="arch" type="xml">
                      <form string="Nhân viên" version="7.0">
                          <header></header>
                          <sheet>
                              <group col="2" string="Thông tin nhân viên">
                                  <field name="name" string="Tên:"/>
                              </group>
                              <group>
                                  <field name="studios" string="Studio phát triển game:"/>
                              </group>
                              <group>
                                  <field name="roles" string="Vai trò:"/>
                              </group>
                          </sheet>
                      </form>
                  </field>
              </record>

              <!-- MEMBER Action -->
              <record model="ir.actions.act_window" id="action_member">
                  <field name="name">Nhân viên</field>
                  <field name="res_model">game.member</field>
                  <field name="view_type">form</field>
                  <field name="view_mode">tree,form</field>
              </record>

              <!-- GENRE Tree View -->
              <record model="ir.ui.view" id="view_genre_tree">
                  <field name="name">genre.tree</field>
                  <field name="model">game.genre</field>
                  <field name="type">tree</field>
                  <field name="arch" type="xml">
                      <tree string="Danh sách thể loại" editable="bottom">
                          <field name="name" string="Tên thể loại"/>
                          <field name="create_date"/>
                          <field name="write_date"/>
                      </tree>
                  </field>
              </record>

              <!-- GENRE Form View -->
              <record model="ir.ui.view" id="view_genre_form">
                  <field name="name">genre.form</field>
                  <field name="model">game.genre</field>
                  <field name="arch" type="xml">
                      <form string="Thể loại Game" version="7.0">
                          <header></header>
                          <sheet>
                              <group col="2">
                                  <field name="name" string="Tên thể loại:"/>
                              </group>
                          </sheet>
                      </form>
                  </field>
              </record>

              <!-- GENRE Action -->
              <record model="ir.actions.act_window" id="action_genre">
                  <field name="name">Thể loại</field>
                  <field name="res_model">game.genre</field>
                  <field name="view_type">form</field>
                  <field name="view_mode">tree,form</field>
              </record>

              <!-- PLATFORM Tree View -->
              <record model="ir.ui.view" id="view_platform_tree">
                  <field name="name">platform.tree</field>
                  <field name="model">game.platform</field>
                  <field name="type">tree</field>
                  <field name="arch" type="xml">
                      <tree string="Danh sách nền tảng" editable="bottom">
                          <field name="name" string="Tên nền tảng"/>
                          <field name="create_date"/>
                          <field name="write_date"/>
                      </tree>
                  </field>
              </record>

              <!-- PLATFORM Form View -->
              <record model="ir.ui.view" id="view_platform_form">
                  <field name="name">platform.form</field>
                  <field name="model">game.platform</field>
                  <field name="arch" type="xml">
                      <form string="Nền tảng" version="7.0">
                          <header></header>
                          <sheet>
                              <group col="2">
                                  <field name="name" string="Tên nền tảng:"/>
                              </group>
                          </sheet>
                      </form>
                  </field>
              </record>

              <!-- PLATFORM Action -->
              <record model="ir.actions.act_window" id="action_platform">
                  <field name="name">Nền tảng</field>
                  <field name="res_model">game.platform</field>
                  <field name="view_type">form</field>
                  <field name="view_mode">tree,form</field>
              </record>

              <!-- SERIES Tree View -->
              <record model="ir.ui.view" id="view_series_tree">
                  <field name="name">series.tree</field>
                  <field name="model">game.series</field>
                  <field name="type">tree</field>
                  <field name="arch" type="xml">
                      <tree string="Danh sách series">
                          <field name="name"/>
                          <field name="create_date"/>
                          <field name="write_date"/>
                      </tree>
                  </field>
              </record>

              <!-- SERIES Form View -->
              <record model="ir.ui.view" id="view_series_form">
                  <field name="name">series.form</field>
                  <field name="model">game.series</field>
                  <field name="arch" type="xml">
                      <form string="Game Series" version="7.0">
                          <header></header>
                          <sheet>
                              <group col="2" string="Thông tin series">
                                  <field name="name" string="Tên series:" colspan="2"/>
                              </group>
                              <notebook>
                                  <page string="Mô tả">
                                      <field name="description" nolabel="1"/>
                                  </page>
                              </notebook>
                          </sheet>
                      </form>
                  </field>
              </record>

              <!-- SERIES Action -->
              <record model="ir.actions.act_window" id="action_series">
                  <field name="name">Series</field>
                  <field name="res_model">game.series</field>
                  <field name="view_type">form</field>
                  <field name="view_mode">tree,form</field>
              </record>

              <!-- ROLE MODEL VIEWS -->
              <record model="ir.ui.view" id="view_role_tree">
                  <field name="name">role.tree</field>
                  <field name="model">game.role</field>
                  <field name="type">tree</field>
                  <field name="arch" type="xml">
                      <tree string="Danh sách vai trò">
                          <field name="name" string="Tên vai trò"/>
                          <field name="create_date"/>
                          <field name="write_date"/>
                      </tree>
                  </field>
              </record>

              <record model="ir.ui.view" id="view_role_form">
                  <field name="name">role.form</field>
                  <field name="model">game.role</field>
                  <field name="arch" type="xml">
                      <form string="Form Vai trò" version="7.0">
                          <group>
                              <field name="name" string="Tên vai trò"/>
                          </group>
                      </form>
                  </field>
              </record>

              <record model="ir.actions.act_window" id="action_role">
                  <field name="name"> Vai trò </field>
                  <field name="res_model">game.role</field>
                  <field name="view_mode">tree,form</field>
              </record>

              <!-- VERSION MODEL VIEWS -->
              <record model="ir.ui.view" id="view_version_tree">
                  <field name="name">version.tree</field>
                  <field name="model">game.version</field>
                  <field name="type">tree</field>
                  <field name="arch" type="xml">
                      <tree string="Danh sách phiên bản">
                          <field name="version_name" string="Số phiên bản"/>
                          <field name="enhancement_notes" string="Thông tin cải tiến"/>
                          <field name="game_id" string="Game"/>
                          <field name="create_date"/>
                          <field name="write_date"/>
                      </tree>
                  </field>
              </record>
              <record model="ir.ui.view" id="view_version_form">
                  <field name="name">version.form</field>
                  <field name="model">game.version</field>
                  <field name="arch" type="xml">
                      <form string="Form Phiên bản" version="7.0">
                          <group>
                              <field name="create_date" invisible="1"/>
                              <field name="version_name" string="Số phiên bản"
                              attrs="{'readonly':[('create_date','!=',False)]}"
                              />
                              <field name="enhancement_notes" string="Thông tin cải tiến"/>
                              <field name="game_id" string="Game"
                              attrs="{'readonly':[('create_date','!=',False)]}"
                              />
                          </group>
                      </form>
                  </field>
              </record>
              <record model="ir.actions.act_window" id="action_version">
                  <field name="name"> Phiên bản </field>
                  <field name="res_model">game.version</field>
                  <field name="view_mode">tree,form</field>
              </record>
          </data>
      </openerp>
      ```

      ### 3.3 Cấu hình Menu - File `game_menu.xml`
      Cấu hình hệ thống Menu cha và các chức năng Action con được tích hợp vào thanh định hướng giao diện của ERP.

      ```xml
      <?xml version="1.0" encoding="utf-8"?>
      <openerp>
          <data>
              <!-- Menu Cha (Main App App) -->
              <menuitem id="game_parent" name="Quản lý Game" icon="STOCK_OPEN"/>

              <!-- Nhóm Quản lý Game (Games, Series, Genres, Platforms) -->
              <menuitem id="menu_game_parent" name="Games" parent="game_parent" sequence="10"/>

              <!-- action_game handles both the Tree list and Form view automatically now -->
              <menuitem action="action_game" id="menu_game_list" name="Danh sách game" parent="menu_game_parent" sequence="10"/>
              <menuitem action="action_version" id="menu_version_list" name="Phiên bản" parent="menu_game_parent" sequence="20"/>
              <menuitem action="action_series" id="menu_series_list" name="Series" parent="menu_game_parent" sequence="30"/>
              <menuitem action="action_genre" id="menu_genre_list" name="Thể loại" parent="menu_game_parent" sequence="40"/>
              <menuitem action="action_platform" id="menu_platform_list" name="Nền tảng" parent="menu_game_parent" sequence="50"/>

              <!-- Nhóm Tổ chức & Nhân sự (Publishers, Studios, Members) -->
              <menuitem id="menu_company_parent" name="Tổ chức &amp; Nhân sự" parent="game_parent" sequence="20"/>

              <menuitem action="action_publisher" id="menu_publisher_list" name="Nhà phát hành" parent="menu_company_parent" sequence="10"/>
              <menuitem action="action_studio" id="menu_studio_list" name="Studio phát triển game" parent="menu_company_parent" sequence="20"/>
              <menuitem action="action_member" id="menu_member_list" name="Nhân viên" parent="menu_company_parent" sequence="30"/>

              <menuitem action="action_role" id="menu_role_list" name="Vai tro" parent="menu_company_parent" sequence="40"/>
          </data>
      </openerp>
      ```

3. # **Nộp bài bảng mềm:** thời gian nộp vào buổi thi cuối kỳ, gồm:

   1. ## ***File báo cáo***

   2. ## ***Module(sourcecode)***

   3. ## ***Video thuyết trình về nội dung sourcecode và Demo***

4. # **Tài liệu tham khảo:**
   1. Tài liệu OpenERP 7.0 Developer Documentation.
