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
