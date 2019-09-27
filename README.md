React js practice through online:


https://codesandbox.io/s/pp0jl9jzq


Define Immutable class:


public final class Student 
{ 
    final String name; 
    final int regNo; 
  
    public Student(String name, int regNo) 
    { 
        this.name = name; 
        this.regNo = regNo; 
    } 
    public String getName() 
    { 
        return name; 
    } 
    public int getRegNo() 
    { 
        return regNo; 
    } 
} 
  
// Driver class 
class Test 
{ 
    public static void main(String args[]) 
    { 
        Student s = new Student("ABC", 101); 
        System.out.println(s.getName()); 
        System.out.println(s.getRegNo()); 
  
        // Uncommenting below line causes error 
        // s.regNo = 102; 
    } 
} 


Difference between HashMap and ConcurrentHashMap

HashMap is the Class which is under Traditional Collection and ConcurrentHashMap is a Class which is under Concurrent Collections, apart from this there are various differences between them which are:

HashMap is non-Synchronized in nature i.e. HashMap is not Thread-safe whereas ConcurrentHashMap is Thread-safe in nature.
HashMap performance is relatively high because it is non-synchronized in nature and any number of threads can perform simultaneously. But ConcurrentHashMap performance is low sometimes because sometimes Threads are required to wait on ConcurrentHashMap.
While one thread is Iterating the HashMap object, if other thread try to add/modify the contents of Object then we will get Run-time exception saying ConcurrentModificationException.Whereas In ConcurrentHashMap we wont get any exception while performing any modification at the time of Iteration.


Spring Boot fallback model:

https://github.com/Netflix/Hystrix/wiki/Configuration#intro

Proxy setting:

		 ReactorResourceFactory reactorResourceFactory = new ReactorResourceFactory();
	        reactorResourceFactory.setUseGlobalResources(true);;
	        reactorResourceFactory.afterPropertiesSet();
	    
		 
	        return new ReactorClientHttpConnector(reactorResourceFactory, httpClient -> httpClient.tcpConfiguration(tcpClient -> {
	            try {
	                final SslContext sslContext = SslContextBuilder.forClient()
	                        .build();
	                tcpClient.secure(t -> t.sslContext(sslContext))
	                        .option(ChannelOption.SO_KEEPALIVE, false)
	                        .option(ChannelOption.CONNECT_TIMEOUT_MILLIS, 5_000);
	                tcpClient = tcpClient.proxy(proxy -> proxy.type(ProxyProvider.Proxy.HTTP).host("phoendcsrvproxy.gdn.syfbank.com").port(8080).build());
	                return tcpClient;
	            } catch (final SSLException ex) {
	                throw new IllegalStateException("Unable to create SSL context", ex);
	            }
	        }));
	        
	        
		

Json Vs Bson
-----------------------------------------
JSON

JavaScript Object Notation (JSON) is an open, human and machine-readable standard that facilitates data interchange, and along with XML is the main format for data interchange used on the modern web. JSON supports all the basic data types you’d expect: numbers, strings, and boolean values, as well as arrays and hashes.


Binary JSON (BSON)

MongoDB represents JSON documents in binary-encoded format called BSON behind the scenes. BSON extends the JSON model to provide additional data types, ordered fields, and to be efficient for encoding and decoding within different languages.

MongoDB, BSON, and JSON

The MongoDB BSON implementation is lightweight, fast and highly traversable. Like JSON, MongoDB's BSON implementation supports embedding objects and arrays within other objects and arrays – MongoDB can even 'reach inside' BSON objects to build indexes and match objects against query expressions on both top-level and nested BSON keys. This means that MongoDB gives users the ease of use and flexibility of JSON documents together with the speed and richness of a lightweight binary format.

Find Days between two dates:


	                date = fmt1.parse(input);		
			System.out.println("date=" + date);
		        DateFormat fmt2 = new SimpleDateFormat("MM/dd/yyyy");
		        String output = fmt2.format(date);
		    
		        Date currentDate = Calendar.getInstance().getTime();

			long diffInMillies = Math.abs(currentDate.getTime() - date.getTime());
			long diff = TimeUnit.DAYS.convert(diffInMillies, TimeUnit.MILLISECONDS);
			


https://community1.pega.com/community/pega-product-support/question/how-covert-julian-date-normal-date-format%C2%A0-example


Set query Params to RestTemplate:

https://stackoverflow.com/questions/8297215/spring-resttemplate-get-with-parameters

Query Param Example:

https://www.mkyong.com/webservices/jax-rs/jax-rs-queryparam-example/


Excel Find the text:

https://www.extendoffice.com/documents/excel/1783-excel-remove-text-before-character.html

Need to update the below Ui Technologies:


-Reactive js

-typescript

-angular js 6

java_buildpack_offline:

memory: 1G
disk_quota: 1G
buildpack: java_buildpack_offline


#Spring batch paraller processing 

https://github.com/spring-projects/spring-batch/blob/master/spring-batch-docs/asciidoc/scalability.adoc
# decemial format:

                DecimalFormat dd=new DecimalFormat("#0.00");
		System.out.println("d3====="+ dd.format(d3));
#BigDecimal precesion scale

               BigDecimal bg=new BigDecimal(d3);
		bg.setScale(2, RoundingMode.HALF_UP);				
		System.out.println("d3-----="+ bg.doubleValue());

# resource
Query timeout:

https://community.oracle.com/message/15109594#15109594


private String getDateFormat(String stDate, String currentFormat, String reqFormat, List<String> invalidDates) {
		logger.info(ivaProperties.getMethodEntry() + "getDateFormat");
		logger.info(" given Date : " + stDate + " currentFormat :" + currentFormat + "reqFormat : " + reqFormat);

		Date startDate = null;
		String reqDate = StringUtils.EMPTY;
		if (StringUtils.isNotEmpty(currentFormat) && StringUtils.isNotEmpty(stDate) && !invalidDates.contains(stDate)
				&& StringUtils.isNotEmpty(reqFormat)) {
			try {
				SimpleDateFormat df = new SimpleDateFormat(currentFormat);
				startDate = df.parse(stDate);
				df.applyPattern(reqFormat);
				reqDate = df.format(startDate);
			} catch (Exception e) {
				logger.error("Problem  from  getDateFormat() ", e);
			}
		}
		logger.info(ivaProperties.getMethodExit() + "getDateFormat");
		return reqDate;
	}
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		SimpleDateFormat df = new SimpleDateFormat("MM-dd-yy");
		Date startDate;
		try {
			startDate = df.parse("06-22-2010");
			df.applyPattern("dd-MMM-yy");
			String reqDate = df.format(startDate);
			System.out.println(reqDate);
		} catch (ParseException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
	}
=========================================================================================

spring  scheduler:

@Scheduled(cron = "${data.scheduler.cron}", zone="${data.scheduler.timezone}")

    cron: "1 5 8 * * THU"
    timezone: America/New_York

===============================================================

spring batch:
JobParametersBuilder builderff = new JobParametersBuilder();
						builder.addDate("date", new Date());
JobExecution jef = jobLauncher.run(importUserJob(S3, versionId, file1feedCount,file2feedCount),
								builder.toJobParameters());
								
								
		public Job importUserJob(S3 sS3, int versionId, int file1Ffeedcount,int file2Ffeedcount) {
		return jobBuilderFactory.get("test1").incrementer(new RunIdIncrementer())
				.start(stepForfile1chemaList(S3, versionId, file1Ffeedcount))
				.next(stepForfile1chemaList4(S3, versionId, file1Ffeedcount)).build();
	}

	public Step stepForfile1chemaList(AmazonS3 secureAmazonS3, int versionId, int feedcount) {
		return stepBuilderFactory.get("stepForfile1SchemaList").<file1ModelData, file2ModelData> chunk(10000)
				.reader(flatFileReaderForfile1(secureAmazonS3, versionId,             feedcount)).processor(processorfile2())
				.writer(writerfile1SchemaList()).build();
	}							
		
		
		
Flat file reader:

public FlatFileItemReader<ModelData> customreader(s3 s, int versionId,
			int feedcount) {
		FlatFileItemReader<ModelData> reader = new FlatFileItemReader<ModelData>();
		
		bucketObj = s.getObject(config.getBucketName(), config.getfile());
		inputStream = bucketObj.getObjectContent();
		// local test start
		reader.setResource(new InputStreamResource(inputStream));
		// reader.setLinesToSkip(1); // To skip the header in the file
		reader.setLineMapper(new customerLineMapper(versionId, feedcount));
		return reader;
	}



=================================================================================


create Data source for jdbctemplate:
https://kodejava.org/how-do-i-create-a-data-source-object-for-jdbctemplate


private static DataSource getDataSource() {
        // Creates a new instance of DriverManagerDataSource and sets
        // the required parameters such as the Jdbc Driver class,
        // Jdbc URL, database user name and password.
        DriverManagerDataSource dataSource = new DriverManagerDataSource();
        dataSource.setDriverClassName(DataSourceDemo.DRIVER);
        dataSource.setUrl(DataSourceDemo.JDBC_URL);
        dataSource.setUsername(DataSourceDemo.USERNAME);
        dataSource.setPassword(DataSourceDemo.PASSWORD);
        return dataSource;
    }
    
 -------------------------------------------------------------------------------------  
 ORA-12505 :TNS listener does not currently know of SID given in connect descriptor
 
 https://stackoverflow.com/questions/30861061/ora-12505-tns-listener-does-not-currently-know-of-sid-given-in-connect-descript
 
 hikari connection timeout works:
 
 https://stackoverflow.com/questions/26875050/behaviour-of-hikari-setconnectiontimeout
 
 Preparestatementsetter:
 
 https://www.tutorialspoint.com/springjdbc/springjdbc_preparedstatementsetter.htm
 
 
 
 spring boot test case for web :
 
 Api calss:
 
@RunWith(SpringRunner.class)
@WebMvcTest(value = APIcLASS.class)
@ContextConfiguration(classes = ApplicaitonCalss.class)


Api calss
	@Autowired
	private MockMvc mockMvc;
	M1(){
	
	MvcResult result = mockMvc.perform(post("/api/v1_0/l").contentType(MediaType.APPLICATION_JSON)
				.content(gson.toJson(reatuesData))).andReturn();
		RespnoeData response = new ObjectMapper().readValue(result.getResponse().getContentAsString(),
				ResponeData.class);

}
 }
 
 
 Service class:
 
 @RunWith(SpringRunner.class)
@WebMvcTest(value = apiclass.class)
@ContextConfiguration(classes = { Applicaiton.class, properties.class })


Excepiton Test case:

Mockito.when(service.getmethod(Mockito.anyObject()))
	.thenThrow(new customExcepiton("Middleware Serice Down"));
	
	

 
