

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
	
	

 
