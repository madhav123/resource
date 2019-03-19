# resource

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
