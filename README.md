1-	Create Controller @RestController=Receptionner les données via des requets http
@RequestMapping = url prefixer dans les méthodes (users)
      Definie les methodes CRUD (controller)  GetMapping PostMapping ….
      
      

2-	Configurer l’application avec la base de données
Application.properties
Spring.datasource.username =root
Spring.datasource.password=
Spring.datasource.url=jdbc :mysql:localhost:3306/dbname
Spring.jpa.hibernate.ddl.auto=update

3-	Public String createUser(@RequestBody UserRequest userRequest) receptionner les donnees depuis l’exterieur



4-	Create Request
5-	Create Response
Modifier la reponse dans le controlleur (public UserResponse createUser(….)
       
      6-presentation layer : usermodelrest -> userrestcontroller (la reception des donnees et la reponse vers le client)
         Service layer : userdto -> usersservice -> userdto
         Data layer : userentity -> userrepository -> MysQl


6-	Create Dto ( implements Serializable ) definie les attribues du table , generate getters and setters

7-	Dans le controlleur, instancer userDto

Public UserResponse  createUser(@RequestBody UserRequest userRequest)
             ( UserDto userDto = new UserDto();
	Passer les informations de userRequest vers userDto 
	BeanUtils.copy…..) passer les informations vers le service
             UserDto createUser = userService.createUser(userDto)
	Instance une reponse 
	UserResponse userResponse = new UserResponse()
	BeanUtils…..(createUser, userResponse)
	Return userResponse ;
8-	Create Service
UserService
Interface * 
UserDto createUser(UserDto userDto)

9-	Create service Impl
Implements UserService
dans le controlleur -> @AutoWired UserService userService (injection de depandance)
dans userserviceImpl -> @Service
10-	Créer une entity implements serializable
@Entity(name= )
Definie les attributs du table

@Id
@GeneratedValue (AI)
@Column(Nullabla=false)
11-	Créer Une Repository 
Add interface CrudRepository (extends ….)
CrudRepository<UserEntity,Long> 

12-	 Dans Repository 

@Repository 

Dans serviceImpl
@AutoWired 
UserRepos…. userRe….
Public UserDto createUser(UserDto user)
Instance une entité 
UserEntity userEntity = new UserEntity()
BeanUtils…..(user,userEntity)
UserEntity newUser = UserRepository.(method(userEntity))
UserDto userDto = new UserDto ()
BeanUtils……(newUser, userDto)
Return userDto;



Methode GET
@PathVariable

Dans le service définie la méthode
UserDto getUserByUserId(String userId)

Implementer dans service impl
Dans repository
UserEntity findByUserId(String userId)

	Dans serviceImp
	UserEntity userEntity = userRepository. findByUserId(userId)

if(userEntity==null) throw null;
UserDto userDto = new UserDto ()
BeanUtils…..(userEntity,userDto);
Return userDto;

Dans Controller
UserDto userDto = UserService. getUserByUserId
Instancer une response

BeanUtils…..;(userDto, userResponse)
Return userResponse;

METHODE PUT 

Definie la methode dans repository OrderEntity findById(Lond id);



Dans le controller, 

la méme procédure  (CREATE USER)
Changer createuser avec updateuser(id,userDto)

Define la methode dans le service
UserDto updateUser(String id,UserDto userDto)
Implementer la methode dans serviceimpl


Dans service impl
UserEntity userEntity = userRepository. findByUserId(userId)

if(userEntity==null) throw null;
userEntiy.setFirstName(userDto.getFirstName)
UserEntity userUpdated = userRepository.save(userEntity);
UserDto user = new UserDto ()
BeanUtils….( userUpdated,user)
Return user;

Methode delete

Dans le service 
Void deleteUser(String userId)
Implementer dans service imp

UserEntity userEntity = userRepository. findByUserId(userId)

if(userEntity==null) throw null;
userRepository.delete(userEntity);

dans controller
userService.deleteUser(id);



------------------------
create new interface mapper
@Mapper(componentModel = "****")


ClientDto entityToModel(ClientEntity source)
ClientEntity modelToEntity(ClientDto destiantion)
@IterableMapping(qualifiedByName = "entityToModel") 
List<ClientDto> entitiesToModels(List<ClientEntity> clients);




	
