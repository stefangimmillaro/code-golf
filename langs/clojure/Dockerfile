FROM clojure:temurin-19-tools-deps-alpine as builder

FROM codegolf/lang-base

ENV JAVA_HOME /opt/java/openjdk

COPY --from=0 / /

RUN mkdir -p  /.clojure/tools    \
 && echo {} > /.clojure/deps.edn \
 && echo {} > /.clojure/tools/tools.edn

ENTRYPOINT ["clojure"]

CMD ["-M", "-e", "(println (clojure-version))"]
