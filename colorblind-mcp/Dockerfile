# Glama / container check for colorblind-mcp.
# Installs the published package and runs it over stdio, which is all the
# introspection check needs (server starts, answers initialize + tools/list).
FROM node:20-alpine
RUN npm install -g colorblind-mcp
CMD ["colorblind-mcp"]
