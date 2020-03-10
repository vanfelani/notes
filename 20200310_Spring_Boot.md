####@Repository
+ Anntotation @Repository mengindikasikan bahwa class yang di beri annotation tersebut adalah Repository.

+ Perbedaan memakai spring boot dan hibernate:
>1. Hibernate

**1. **Ketika melakukan query pada repository membutuhkan entity manager.
Contoh code:
~~~java
private final Class<E> entityClass;
protected final EntityManager entityManager;

public AbstractRepository(Class<E> entityClass, EntityManager entityManager) {
      this.entityClass = entityClass;
      this.entityManager = entityManager;
}
~~~

**2. ** Ketika melakukan transaksi membutuhkan transaction.begin() dan transaction.commit().
Contoh code:
~~~java
public Stock save(Stock entity) throws SQLException {
     EntityTransaction transaction = entityManager.getTransaction();
     transaction.begin();

     Stock result = repository.save(entity);
     transaction.commit();

     return result;
}
~~~

Dua kalimat di atas merupakan implementasi pada hibernate.

>2. Spring Boot

**1. ** Menyediakan annotation @Autowired yang sudah membungkus entity manager.
Contoh penggunaan annotation @autowired: 
~~~java
@Autowired
private EntityManager entityManager;
~~~

**2. ** Menyediakan annotation @Transactional yang membungkus transaction.begin() dan transaction.commit(). Annotation ini dapat diletakkan pada class ataupun method, Sehingga ketika class atau method yang mempunyai annotation @Transactional terdapat error maka class atau method tersebut akan melakukan rollback.
Contoh penggunaan annotation @Transactional pada class:
~~~java
@Transactional
@Service
public class ItemServiceImpl implements ItemService {}
~~~

Contoh penggunaan annotation @Transactional pada method:
~~~java
@Transactional
@Override
public Item findById(Integer id) {
    return repository.findById(id).orElseThrow(() -> {
        return new EntityNotFoundException();
    });
}
~~~

+ Annotation @Transactional memiliki nilai default require, ketika di panggil di luar transactional context maka interceptor harus memulai transaksi baru.

+ Tipe transaction *mandatory* harus dipanggil di transaction context karena tidak ada transaction.begin() dan transaction.commit().

####Custom Repository
**1. ** Membuat interface ItemRepositoryCustom
~~~java
public interface ItemRepositoryCustom {
    public List<Item> findByNameLike(String name);
}
~~~

**2. ** Karena interface ItemRepository sudah melakukan extend pada JpaRepository, maka interface ItemRepositoryCustom dapat diletakkan pada extends ItemRepository sehingga interface ItemRepositoryCustom sudah memiliki semua method dari JpaRepository dan menjadi repository.
~~~java
public interface ItemRepository extends JpaRepository<Item, Integer>, ItemRepositoryCustom{
    public List<Item> findByNameContaining(String name);
}
~~~

**3. ** Buat class ItemRepositoryCustomImpl yang mengimplement ItemRepositoryCustom agar class ItemRepositoryCustomImpl menjadi repository dan mempunyai method dari JpaRepository.
~~~java
public class ItemRepositoryCustomImpl implements ItemRepositoryCustom {

    @Autowired
    private EntityManager entityManager;

    @Override
    public List<Item> findByNameLike(String name) {
        CriteriaBuilder builder = entityManager.getCriteriaBuilder();
        CriteriaQuery<Item> query = builder.createQuery(Item.class);
        Root<Item> root = query.from(Item.class);
        query.where(builder.like(root.get("name"), "%" + name + "%"));
        return entityManager.createQuery(query).getResultList();
    }
}
~~~

**4. ** Buat class interface ItemService yang mempunyai method findByNameLike().
~~~java
public interface ItemService {
	public List<Item> findByNameLike(String name, boolean ignoreCase);
}
~~~

**5. ** Panggil method findByNameLike() pad class Item Controller.
~~~java
@GetMapping
public ResponseMessage<List<ItemModel>> findAll(@RequestParam(required = false) String name, boolean ignoreCase) {
    List<Item> items = name != null ? itemService.findByNameLike(name, ignoreCase) : itemService.findAll();

    ModelMapper modelMapper = new ModelMapper();
    Type type = new TypeToken<List<ItemModel>>() {}.getType();
    List<ItemModel> models = modelMapper.map(items, type);

    return ResponseMessage.success(models);
}
~~~

####Query By Example
+ Query by Example (QBE) adalah metode pembuatan query yang memungkinkan kita untuk mengeksekusi query berdasarkan example entity instance. QBE ini berguna untuk melakukan pencarian.

Contoh Penggunaan QBE:
**1. ** Buat method yang mengimplemtasikan QBE sebagai contoh adalah method findAll
~~~java
@Override
public List<Item> findAll(Item entity) {
    ExampleMatcher matcher = ExampleMatcher.matchingAll()
            .withIgnoreCase()
            .withStringMatcher(ExampleMatcher.StringMatcher.CONTAINING);
    return repository.findAll(Example.of(entity,matcher));
}
~~~

**2. ** Buat method findAll pada interface
~~~java
public List<Item> findAll(Item entity);
~~~

**3. ** Gunakan method findAll pada class ItemController
~~~java
@GetMapping
public ResponseMessage<List<ItemModel>> findAll(@RequestParam(required = false) String name) {
    Item entity = new Item(name);
    List<Item> items = itemService.findAll(entity);

    ModelMapper modelMapper = new ModelMapper();
    Type type = new TypeToken<List<ItemModel>>() {}.getType();
    List<ItemModel> models = modelMapper.map(items, type);

    return ResponseMessage.success(models);
}
~~~

####Pagination
+ Pagination sangat berguna ketika memiliki data yang besar dan ingin menyajikan kepada pengguna dalam potongan yang lebih kecil, dan juga ketika perlu mengurutkan data berdasarkan beberapa kriteria saat paging.

+ Interface Page memiliki:
	- Method getTotalElement untuk mengetahui total element.
	- Method getTotalPage untuk mengetahui total halaman.
	- Method getNumberofSize untuk mengetahui size pada satu halaman.
	- Method getSize untuk mengetahui size berdasarkan url.

+ Implementasi pagination
**1. ** Buat method pada class interface ItemService.
~~~java
public interface ItemService {
   public Page<Item> findAll(Item entity, int page, int size, Sort.Direction direction);
}
~~~

**2. ** Implementasikan method pada ItemService di class ItemServiceImpl.
~~~java
@Override
public Page<Item> findAll(Item entity, int page, int size, Sort.Direction direction) {
    Sort sort = Sort.Direction.DESC.equals(direction) ? Sort.by(direction, "id").descending() : Sort.by("id");
    ExampleMatcher matcher = ExampleMatcher.matchingAll()
            .withIgnoreCase()
            .withStringMatcher(ExampleMatcher.StringMatcher.CONTAINING);
    return repository.findAll(Example.of(entity, matcher), PageRequest.of(page, size, sort));
}
~~~

**3. ** Buat class PageableList.
~~~java
public class PageableList<T> {

    private List<T> list;
    private Integer page;
    private Integer size;
    private long total;

    public PageableList(List<T> list, Integer page, Integer size, long total) {
        this.list = list;
        this.page = page;
        this.size = size;
        this.total = total;
    }

    public List<T> getList() {
        return list;
    }

    public void setList(List<T> list) {
        this.list = list;
    }

    public Integer getPage() {
        return page;
    }

    public void setPage(Integer page) {
        this.page = page;
    }

    public Integer getSize() {
        return size;
    }

    public void setSize(Integer size) {
        this.size = size;
    }

    public long getTotal() {
        return total;
    }

    public void setTotal(long total) {
        this.total = total;
    }
}
~~~

**4. ** Gunakan method pada ItemController.
~~~java
@GetMapping
public ResponseMessage<PageableList<ItemModel>> findAll(
        @RequestParam(required = false) String name,
        @RequestParam(defaultValue = "asc") String sort,
        @RequestParam(defaultValue = "0") int page,
        @RequestParam(defaultValue = "10") int size
) {
    if (size > 100) {
        size = 100;
    }
    Item entity = new Item(name);
    Sort.Direction direction = Sort.Direction
            .fromOptionalString(sort.toUpperCase())
            .orElse(Sort.Direction.ASC);
    Page<Item> pageItems = itemService.findAll(entity, page, size, direction);
    List<Item> items = pageItems.toList();

    ModelMapper modelMapper = new ModelMapper();
    Type type = new TypeToken<List<ItemModel>>() {}.getType();
    List<ItemModel> itemModels = modelMapper.map(items, type);
    PageableList<ItemModel> data = new PageableList(itemModels, pageItems.getNumber(),
                pageItems.getSize(), pageItems.getTotalElements());

    return ResponseMessage.success(data);

}
~~~