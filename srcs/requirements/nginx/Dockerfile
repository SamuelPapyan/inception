# **************************************************************************** #
#                                                                              #
#                                                         :::      ::::::::    #
#    Dockerfile                                         :+:      :+:    :+:    #
#                                                     +:+ +:+         +:+      #
#    By: spapyan <spapyan@student.42.fr>            +#+  +:+       +#+         #
#                                                 +#+#+#+#+#+   +#+            #
#    Created: 2024/02/08 17:14:51 by spapyan           #+#    #+#              #
#    Updated: 2024/02/08 17:14:51 by spapyan          ###   ########.fr        #
#                                                                              #
# **************************************************************************** #

FROM alpine:3.19
RUN	apk update && apk upgrade && apk add --no-cache nginx
EXPOSE 443
CMD ["nginx", "-g", "daemon off;"]
